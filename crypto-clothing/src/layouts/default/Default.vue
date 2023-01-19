<template>
  <v-app>
    <default-bar class="app-bar" />

    <default-view class="default-view mt-2"/>
  </v-app>
</template>

<script setup>
  import DefaultBar from './AppBar.vue'
  import DefaultView from './View.vue'
</script>

<style scoped>
.app-bar {
  z-index: -1;
}

.default-view {
  z-index: 0;
}

</style>