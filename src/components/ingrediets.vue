<template>
  <div>
  <section>
    <input type="text" v-model="data.filter" placeholder="Type something to filter the list" />
  </section>
  <section>
    <input type="text" v-model="data.newIngredient" placeholder="Title" />
    <button @click="add(data.newIngredient)" @disabled="!data.newIgredient">Add</button>
  </section>
  <section>
    <template v-if="!data.ingredients.length">
      <h1>No ingredients found</h1>
    </template>
    <template v-else>
      <table>
        <thead>
          <tr>
            <th>#</th>
            <th>Name</th>
            <th></th>
          </tr>
        </thead>
        <div >
          <div v-for="ingredient in filteredIngredients" :key="ingredient" class="bg-dark">
            <p>{{ingredient.id}}</p>
            <p>{{ingredient.name}}</p>
            <div>
              <button @click="update(ingredient)" class="btn btn-dark">Update</button>
              <button @click="remove(ingredient)">Delete</button>
            </div>
          </div>
        </div>
      </table>
    </template>
  </section>
  </div>
</template>

<script>
import { reactive, computed } from "vue";
import { useStore } from "../store";
export default {
  setup() {
    const store = useStore();
    const data = reactive({
      ingredients: store.ingredients,
      filter: "",
      newIngredient: ""
    });
    const filteredIngredients = computed(() =>
      data.ingredients.filter(
        ingredient => !data.filter || ingredient.name.includes(data.filter)
      )
    );
    const add = ingredient => {
      store.addIngredient(ingredient);
    };
    const update = ingredient => {
      data.newIngredient = ingredient;
      rmeove(ingredient);
    };
    const remove = ingredient => {
      store.removeIngredient(ingredient);
    };
    return {
      filteredIngredients,
      data,
      add,
      update,
      remove
    };
  }
};
</script>
