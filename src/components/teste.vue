

 <table>
 <Message :msg="msg" v-show="msg" />
      <tr>
        <th>#:</th>
        <th>Cliente</th>
        <th>Pao</th>
        <th>Carne</th>
        <th>Opcionais</th>
        <th>Ações:</th>
      </tr>

      <tr v-for="burger in burgers" :key="burger.id" id="burger-table-row">
        <td>{{ burger.id }}</td>
        <td>{{ burger.nome }}</td>
        <td>{{ burger.pao }}</td>
        <td>{{ burger.carne }}</td>
        <td>
          <ul>
            <li v-for="(opcional, index) in burger.opcionais" :key="index">
              {{ opcional }}
            </li>
          </ul>
        </td>
        <td>
          <select name="status"
              
              @change="updateBurger($event, burger.id)">
            <option value="">solicitado</option>
            <option
                :value="stats.tipo"
                :selected="burger.status == stats.tipo"
                v-for="stats in status"
                :key="stats.id"
                >{{ stats.tipo }}
              </option>
          </select>
          <button class="delete-btn" @click="deleteBurger(burger.id)">
              Cancelar
            </button>
        </td>
      </tr>
    </table>

    
      <div id="burger-table">
    <Message :msg="msg" v-show="msg" />
    <div>
      <div id="burger-table-heading">
        <div class="order-id">#:</div>
        <div>Cliente</div>
        <div>Pao</div>
        <div>Carne</div>
        <div>Opcionais</div>
        <div>Ações:</div>
      </div>
      <div id="burger-table-rows">
        <div
          class="burger-table-row"
          v-for="burger in burgers"
          :key="burger.id"
        >
          <div class="order-number">{{ burger.id }}</div>
          <div>{{ burger.nome }}</div>
          <div>{{ burger.pao }}</div>
          <div>{{ burger.carne }}</div>
          <div>
            <ul>
              <li v-for="(opcional, index) in burger.opcionais" :key="index">
                {{ opcional }}
              </li>
            </ul>
          </div>
          <div>
            <select
              name="status"
              class="status"
              @change="updateBurger($event, burger.id)"
            >
              <option value="">Selecione</option>
              <option
                :value="stats.tipo"
                :selected="burger.status == stats.tipo"
                v-for="stats in status"
                :key="stats.id"
                >{{ stats.tipo }}
              </option>
            </select>
            <button class="delete-btn" @click="deleteBurger(burger.id)">
              Cancelar
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>


  
#burger-table {
  height: 100vh;
  max-width: 1200px;
  margin: 0 auto;
}

#burger-table-heading,
#burger-table-rows,
.burger-table-row {
  display: flex;
  flex-wrap: wrap;
}

#burger-table-heading {
  font-weight: bold;
  padding: 12px;
  border-bottom: 3px solid #333;
}

#burger-table-heading div,
.burger-table-row div {
  width: 19%;
}

.burger-table-row {
  width: 100%;
  padding: 12px;
  border-bottom: 1px solid #ccc;
}

#burger-table-heading .order-id,
.burger-table-row .order-number {
  width: 5%;
}

select {
  padding: 12px 6px;
  margin-right: 12px;
}

.delete-btn {
  background: #222;
  color: #fcba03;
  border: 2px solid #222;
  cursor: pointer;
  padding: 10px;
  transition: 0.5s;
}
.delete-btn:hover {
  background: transparent;
  color: #222;