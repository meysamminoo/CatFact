<template>
  <v-container fluid>
    <HelloWorld />
    <div v-for="name in animelist" :key="name">
      <p>{{ name.text }}</p>
    </div>
  </v-container>
</template>

<script setup>
import HelloWorld from "@/components/HelloWorld.vue";
import { onMounted, reactive } from "vue";
import axios from "axios";

let animelist = reactive([]);

function test() {
  axios
    .get(
      "https://cat-fact.herokuapp.com/facts/random?animal_type=cat&amount=2",
      {
        "Content-Type": "application/json",
      }
    )
    .then((res) => {
      console.log(res);
      animelist = [...res.data];
    });
}

onMounted(() => {
  console.log(`the component is now mounted.`);
  test();
});
</script>
