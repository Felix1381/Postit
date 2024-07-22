<template>
  <div class="home">
    <Sticky />
  </div>
</template>

<script>
// @ is an alias to /src
import Sticky from "@/components/StickyComponent.vue";
//import Formulaire from "@/components/Formulaire.vue";
export default {
  name: "HomeView",
  components: {
    //Formulaire,
    Sticky,
  },
};
</script>
