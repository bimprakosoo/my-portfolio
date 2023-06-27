<template>
  <v-app-bar app color="#262A56" dark flat class="px-12 custom-navbar">
    <div class="d-flex justify-center w-100">
    <v-btn text @click="scroll('home')" class="text-yellow">Home</v-btn>
    <v-btn text @click="scroll('skill')" class="text-grey">Skill</v-btn>
    <v-btn text @click="scroll('portfolio')" class="text-grey">Portfolio</v-btn>
    </div>
  </v-app-bar>
</template>

<script>
export default {
  methods : {
    scroll(refName) {
      const element = document.getElementById(refName);
      element.scrollIntoView({behavior: "smooth"});
    }
  }
}
</script>
<style scoped>
.custom-navbar .v-btn {
  display: flex;
  justify-content: center;
}
</style>