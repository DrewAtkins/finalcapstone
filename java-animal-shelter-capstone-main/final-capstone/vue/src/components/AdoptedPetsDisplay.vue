<template>
  <div id="adopted-pets">
    <div class="head2">
      <header-area />
    </div>
    <div class="logged-in-view">
      <logged-in-view />
    </div>
    <h1>Adopted Pets</h1>
    <div id="pets-display">
      <pet-card
        id="pet-card"
        v-for="pet in filteredList"
        v-bind:key="pet.id"
        v-bind:pet="pet"
      />
    </div>

    <div class="footer2">
      <footer-area />
    </div>
  </div>
</template>

<script>
import petServices from "@/services/PetServices.js";
import PetCard from "@/components/PetCard.vue";

import HeaderArea from "@/components/HeaderArea.vue";
import FooterArea from "@/components/FooterArea.vue";
import LoggedInView from "@/views/LoggedInView.vue";

export default {
  name: "adopted-pets",
  components: {
    PetCard,
    HeaderArea,
    FooterArea,
    LoggedInView,
  },
  created() {
    petServices.displayPets().then((response) => {
      this.$store.state.pets = response.data;
    });
  },
  computed: {
    filteredList() {
      let adoptedPets = this.$store.state.pets.filter(
        (pet) => pet.is_adoptable === false
      );
      return adoptedPets;
    },
  },
};
</script >

<style >
#pets-display {
  text-align: center;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  margin-bottom: 100px;
}
.head2 {
  margin-bottom: 80px;
}

h1 {
  margin-bottom: 90px;
}
</style>