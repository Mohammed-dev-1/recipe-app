<template>
  <nav>
    <router-link to="/">Recipe App</router-link>
    <ul>
      <li v-for="route in routes" :key="route.path">
        <router-link :to="route.to" :class="{ active: isActive(route.to) }">{{route.text}}</router-link>
      </li>
    </ul>
  </nav>
</template>

<script>
import { computed } from "vue";
import { useRouter } from "vue-router";
export default {
  setup() {
    const routes = [
      { to: "/ingredients", text: "Ingredients" },
      { to: "/recipes", text: "Recipes" }
    ];
    const router = useRouter();
    const activeRoute = computed(() => router.currentRoute.value.path);
    const isActive = path => path === activeRoute.value;
    return { isActive, routes };
  }
};
</script>

<style scoped>
nav{
  padding: 10px;
}
  ul{
    list-style: none;
    display: flex;
    padding: 20px;
    background: darkslategray;
    border: 2px solid lightslategray;
}
ul li {
  margin-left: 20px;
}
ul a {
  color: lightgray;
  text-decoration: none;
}
a {
  color: darkcyan;
  text-decoration: none;
}
</style>