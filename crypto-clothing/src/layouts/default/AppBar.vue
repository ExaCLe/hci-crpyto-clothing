<template>
  <v-app-bar height="150" class="app-bar">
    <v-app-bar-title>
      <p @click="$router.push('/')" class="text-lg-h2">Crypto Clothing</p>
    </v-app-bar-title>
    <p @click="$router.push('/outfits')" class="text-lg-h6">Outfits</p>
    <v-spacer/> 
    <v-icon class="pa-10 icon">mdi-magnify</v-icon>
    <v-icon class="pa-10 icon">mdi-cart-outline</v-icon>
    <p class="text-lg-h6 pa-10 mr-30">Login</p>
  </v-app-bar>
</template>

<script setup>
</script>
<style scoped>
.app-bar {
  z-index: 2;
}
p:hover, .icon:hover {
  cursor: pointer;
}
</style>
