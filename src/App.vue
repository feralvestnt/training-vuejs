<template>
  <!--<div>
    Root Foo: {{rootFoo}} <br />
    Robots Foo: {{robotsFoo}} <br />
    Users Foo: {{usersFoo}} <br />
    <br />
    Root Getter Foo: {{rootGetterFoo}} <br />
    Robots Getter Foo: {{robotsGetterFoo}} <br />
  </div>-->
  <header>
    <nav>
      <ul>
        <li class="nav-item" >
          <router-link class="nav-link" :to="{name: 'Home'}" exact>
          <img class="logo" src="./assets/build-a-bot-logo.png" />
          build-a-bot
          </router-link>
        </li>
        <li class="nav-item" >
          <router-link class="nav-link" :to="{name: 'Build'}" exact>
            Build
          </router-link>
        </li>
        <li class="nav-item cart" >
          <router-link class="nav-link" to="/cart" exact>
            Cart
          </router-link>
          <div class="cart-items">
            {{cart.length}}
          </div>
        </li>
        <li>
          User: {{user.userName}}
          <button @click="changeUserName()" > Change User</button>
        </li>
      </ul>
    </nav>
  </header>
  <div class="container">
    <aside class="aside" > 
      <router-view name="sidebar" />
    </aside>
    <main>
      <router-view/>
    </main>
  </div>
</template>
<script>

import { mapState, mapGetters } from 'vuex';

export default {
  name: 'App',
  computed: {
    ...mapState({ 
      rootFoo: 'foo', 
      usersFoo: state => state.users.foo
    }),
    ...mapState('robots', { robotsFoo: 'foo' }), // this sintax works only when a module has namespace defined
    ...mapGetters({ rootGettersFoo: 'foo' }),
    ...mapGetters('robots', { robotsGetterFoo: 'foo' }),
    cart() {
      return this.$store.state.robots.cart;
    }
  },
  data() {
    return {
      user: { userName: 'Fernando Henrique Alves'},
    };
  },
  provide() {
    return { user: this.user };
  },
  methods: {
    changeUserName() {
      this.user.userName = 'Teste User';
    }
  }
};
</script>

<style>
body {
  background: #999;
  background-attachment: fixed;
}
</style>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
main {
  padding: 30px;
  background-color: white;
  width: 964px;
  min-height: 300px;
}
header {
  background-color: #999;
  width: 1184px;
  margin: 0 auto;
}
ul {
  padding: 3px;
  display: flex;
}
.nav-item {
  display: inline-block;
  padding: 5px 10px;
  font-size: 22px;
  border-right: 1px solid #bbb;
}
.logo {
  vertical-align: middle;
  height: 30px;
}
.nav-link {
  text-decoration: none;
  color: inherit;
}
.router-link-active {
  color: white;
}
.container {
  display: flex;
  margin: 10px auto 0 auto;
  justify-content: center;
}
.aside {
  padding: 30px;
  background-color: #aaa;
  width: 100px;
  min-height: 300px;
}
.nav-item.cart {
  position: relative;
  margin-left: auto;
  border-right: none;
}
.cart-items {
  position: absolute;
  top: -5px;
  right: -9px;
  font-size: 18px;
  width: 20px;
  text-align: center;
  display: inline-block;
  border-radius: 100px;
  background-color: mediumseagreen;
}
</style>
