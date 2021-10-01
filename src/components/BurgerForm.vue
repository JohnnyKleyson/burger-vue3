<template>
  <div>
    <div>
      <Message :msg="msg" v-show="msg" />
      <form id="burger-form" @submit="createBurger">
        <div class="input-container">
          <label for="nome">Seu Nome</label>
          <input
            type="text"
            id="nome"
            name="nome"
            v-model="nome"
            placeholder="Insira seu Nome"
          />
        </div>

        <div class="input-container">
          <label for="pao">Escolha o Pão</label>
          <select name="pao" id="pao" v-model="pao">
            <option value="">Selecione o seu Pão</option>
            <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">
              {{ pao.tipo }}
            </option>
          </select>
        </div>

        <div class="input-container">
          <label for="carne">Escolha a carne:</label>
          <select name="carne" id="carne" v-model="carne">
            <option value="">Selecione o tipo de carne</option>
            <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">
              {{ carne.tipo }}
            </option>
          </select>
        </div>

        <div class="input-container" id="opcionais-container">
          <label for="opcionais">Selecione os Opcionais:</label>
          <div
            class="checkbox-container"
            v-for="opcional in opcionaisdata"
            :key="opcional.id"
          >
            <input
              type="checkbox"
              name="opcionais"
              id="opcionais"
              v-model="opcionais"
              :value="opcional.tipo"
            />
            <span>{{ opcional.tipo }}</span>
          </div>
        </div>

        <div class="input-container">
          <input type="submit" class="submit-btn" value="CRIAR MEU BURGER!" />
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import Message from "./Message.vue";

export default {
  name: "BurgerForm",
  components: {
    Message,
  },
  data() {
    return {
      paes: null,
      carnes: null,
      opcionaisdata: null,
      nome: null,
      pao: null,
      carne: null,
      opcionais: [],
      msg: null,
    };
  },
  methods: {
    async getIngredientes() {
      const req = await fetch("http://localhost:3000/ingredientes");
      const data = await req.json();

      this.paes = data.paes;
      this.carnes = data.carnes;
      this.opcionaisdata = data.opcionais;
      console.log(data);
    },

    async createBurger(e) {
      e.preventDefault();
      const data = {
        nome: this.nome,
        carne: this.carne,
        pao: this.pao,
        opcionais: Array.from(this.opcionais),
        status: "Solicitado",
      };
      console.log("criou o hamburger", data);

      const dataJson = JSON.stringify(data);
      const req = await fetch("http://localhost:3000/burgers", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: dataJson,
      });
      //resposta do backend em forma de const
      const res = await req.json();
      console.log(res);

      this.msg = `Pedido N${res.id} Realizado com sucesso`;
      //limpar msg
      setTimeout(() => (this.msg = ""), 3000);

      this.nome = "";
      this.carne = "";
      this.pao = "";
      this.opcionais = "";
    },
  },

  //quando o componente carrega, joga os dados no form
  mounted() {
    this.getIngredientes();
  },
};
</script>

<style scoped>
#burger-form {
  /*background-color: teal;*/
  border-radius: 25px;
  padding: 30px;
  max-width: 400px;
  margin: 0 auto;
}

.input-container {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}

label {
  font-weight: bold;
  color: black;
  padding: 5px 10px;
  border-left: 3px solid #fcba03;
}
input,
select {
  background: #ddd;
  margin-top: 8px;
  border: none;
  padding: 5px;
  outline: none;
  font-size: 15px;
  border-radius: 5px;
  padding: 5px 10px;
}
#opcionais-container {
  flex-direction: row;
  flex-wrap: wrap;
}
.checkbox-container {
  display: flex;
  align-items: flex-start;
  width: 50%;
  margin-bottom: 20px;
}
.checkbox-container span,
.checkbox-container input {
  width: auto;
}
.checkbox-container span {
  margin-left: 6px;
  font-weight: bold;
}

.submit-btn {
  font-weight: bold;
  letter-spacing: 2px;
  background-color: #222;
  color: #fcba03;
  border: none;
  padding: 10px;
  border-radius: 10px;
  cursor: pointer;
  transition: 0.4s;
}

.submit-btn:hover {
  background: #fff;
  color: #222;
  border: 1px solid black;
}
</style>
