<template>
  <header :class="{ 'scrollew-nav': scrollPosition }">
    <nav>
      <div class="branding"><img src="/img/logo.png" alt="" /></div>
      <ul v-show="!mobile" class="navigation">
        <li><router-link class="link" :to="{name: 'Home'}">Home</router-link></li>
        <li><router-link class="link" :to="{name: ''}">Pedidos</router-link></li>
        <li><router-link class="link" :to="{name: ''}">Contact</router-link></li>
      </ul>
      <div class="icon">
      <i v-show="mobile" class="far fa-bars" @click="toggleMobileNav" :class="{'icon-active': mobileNav}"></i>
      </div>
      <transition name="mobile-nav">
       <ul v-show="mobileNav" class="dropdown-nav">
        <li><router-link class="link" :to="{name: 'Home'}">Home</router-link></li>
        <li><router-link class="link" :to="{name: ''}">Pedidos</router-link></li>
        <li><router-link class="link" :to="{name: ''}">Contact</router-link></li>
      </ul>
      </transition>
    </nav>
  </header>
</template>

<script>
export default {
    name:'Navigation'
}
</script>
