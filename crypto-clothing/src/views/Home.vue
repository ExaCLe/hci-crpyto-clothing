<template>
  <v-container fluid>
    <v-row>
      <v-img src="../assets/Model1.png" class="hover-img"/>
      <v-img src="../assets/Model2.png" class="hover-img"/>
      <v-img src="../assets/Model3.png" class="hover-img"/>
      <v-img src="../assets/Model4.png" class="hover-img"/>
      <v-img src="../assets/Model5.png" class="hover-img"/>
    </v-row>
    <v-container align="center" justify="center">
      <v-btn color="primary" class="mt-10" @click="$router.push('/outfits')">Outfit erstellen</v-btn>
    </v-container>
  </v-container>
</template>

<script>

</script>
<style lang="scss">
@import './../styles/image_hover.css';
</style>
