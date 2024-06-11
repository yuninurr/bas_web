<script setup>
import { reactive } from "vue";
import { RouterLink, RouterView } from "vue-router";
import Header from "./components/Header.vue";
import HelloWorld from "./components/HelloWorld.vue";
import { useAuthStore } from "./stores/auth";

const auth = useAuthStore();

const data = reactive({
  // variable1: 'Be Rich',
  counter: 1,
  variable2: [1, 2, 3, 4],
});

const tambahCounter = () => {
  data.counter++;
};
</script>

<template>
  <header>
    <img
      alt="Vue logo"
      class="logo"
      src="@/assets/yuni-formal.jpg"
      width="150"
      height="150"
    />
    <div class="wrapper">
      <Header :text="' Hai, Good Morning'">
        <button @click="tambahCounter">Tambah Counter</button>
        <p>Saya banyak duit</p>
        <p>{{ data.counter }}</p>
        <!-- <p>Test paragraph in slot</p> -->
        <!-- <template #part1_header="{ param1 }">
          <h2>{{ param1 }}</h2>
        </template> -->
      </Header>

      <HelloWorld msg="Yuni Nur !" />
      {{ data.variable1 }}

      <nav>
        <RouterLink v-if="auth.isLoggedIn" to="/">Home</RouterLink>
        <RouterLink v-if="auth.isLoggedIn" to="/about">About</RouterLink>
        <RouterLink v-if="!auth.isLoggedIn" to="/login">Login</RouterLink>
        <RouterLink v-if="!auth.isLoggedIn" to="/transfer">Transfer</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 200vh;
  background-color: #A7D2CB;
  color: #056676;
  /*rounded style*/
  border-radius: 20px;
  padding-left: 30px;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
  /*line border radius*/
  border-radius: 30%;
  border: 3px solid #55ad9b;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
