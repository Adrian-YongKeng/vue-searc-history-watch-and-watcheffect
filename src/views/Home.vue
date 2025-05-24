<!-- <template> -->
  <!-- <div class="home">home</div> -->
  <!-- <p ref="p">My name is {{ name }} and my age is {{ age }}</p> -->
  <!-- <p>My name is {{ name }} and my age is {{ age }}</p> -->

  <!-- <button @click="handleClick">Click me</button> -->
  <!-- <button @click="age++">Add 1 to age</button> -->
  <!-- <input type="text" v-model="name" /> -->
<!-- </template> -->
<!-- outside setup , in template no need .value automatically props value  -->
 
<!-- <script>
import { ref } from "vue";

export default {
  name: "Home",
  setup() {
    console.log("setup");

    const p = ref(null);
    console.log(p, p.value);

    const name = ref("mario"); // in setup data not reactive like in data() so use ref to become reactive
    const age = ref(30);

    const handleClick = () => {
      console.log(p, p.value);
      p.value.classList.add("test");
      p.value.textContent = " Hello Ninja";
      name.value = "Luligi";
      age.value = 35;
    };

    return { name, age, handleClick };
  },
  created() {
    console.log("created");
  },
  mounted() {
    console.log("mounted");
  },
};
</script> -->


<!-- <template>
  <div class="home">
    <h1>Home</h1>
    <h2>Refs</h2>
    <p>{{ ninjaOne.name }} - {{ ninjaOne.age }}</p>
    <button @click="updateNinjaOne">Update Ninja One</button>

    <h2>Reactive</h2>
    <p>{{ ninjaTwo.name }} - {{ ninjaTwo.age }}</p>
    <button @click="updateNinjaTwo">Update Ninja Two</button>
  </div>
</template>
 
<script>
import { ref, reactive } from "vue";

export default {
  name: "Home",
  setup() {
    const ninjaOne = ref({ name: "mario", age: 30 });
    const ninjaTwo = reactive({ name: "luligi", age: 35 });

    const updateNinjaOne = () => {
      ninjaOne.value.age = 40;
    };

    const updateNinjaTwo = () => {
      ninjaTwo.age = 40; //use reactive can access the property directly // but ref work better
    };

    return { ninjaOne, updateNinjaOne, ninjaTwo, updateNinjaTwo };
  },
};
</script> -->

<template>
  <div class="home">
    <h1>Home</h1>
    <input type="text" v-model="search" />

    <p>search term - {{ search }}</p>
    <div v-for="name in matchingNames" :key="name">{{ name }}</div>

    <button @click="handleClick">Stop watching</button>
  </div>
</template>

<script>
import { computed, ref, watch, watchEffect } from "vue";

export default {
  name: "Home",
  setup() {
    const search = ref("");
    const names = ref(["mario", "yoshi", "toad", "adr", "koopa", "bowser"]);

    //if dont want use that value in the func or dont want to run for the first time use watch
    const stopWatch = watch(search, () => {
      console.log("watch func");
    });

    const stopEffect = watchEffect(() => {
      console.log("watcheffect func run"); // run initial when component first load/ setup func first run
      console.log("watcheffect func run", search.value); // using value inside func
    });

    const matchingNames = computed(() => {
      return names.value.filter((name) => name.includes(search.value));
    });

    const handleClick = () => {
      stopWatch(), stopEffect();
    };

    return { names, search, matchingNames, handleClick };
  },
};
</script>
