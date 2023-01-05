<template>
    <OutfitFilters v-model="showFilters"/> 

    <v-container v-if="!showFilters" fluid>
        <v-row class="ma-5">
            <p class="text-lg-h4">Outfits</p>
            <v-spacer/>
            <v-btn color="primary" @click="showFilters = true">Filter</v-btn>
            <v-btn color="primary" class="ml-10">Ohne Vorlage anfangen</v-btn>
        </v-row>
        <v-row>
            <v-img src="../assets/Model6.png" class="hover-img" @click="this.$router.push('/outfits/1')"/>
            <v-img src="../assets/Model7.png" class="hover-img" @click="this.$router.push('/outfits/2')"/>
            <v-img src="../assets/Model8.png" class="hover-img" @click="this.$router.push('/outfits/3')"/>
            <v-img src="../assets/Model9.png" class="hover-img" @click="this.$router.push('/outfits/4')"/>
            <v-img src="../assets/Model10.png" class="hover-img" @click="this.$router.push('/outfits/5')"/>
        </v-row>
        <v-row justify="center" class="mt-15"><p class="text-lg-h6">Wähle einen Vorschlag und passe ihn dann an.</p></v-row>
    </v-container>
</template>
<script>
import OutfitFilters from '../components/OutfitFilters.vue'

export default {
    components: {
        OutfitFilters
    }, 
    data() {
        return {
            showFilters: true, 
        }
    }, 
}
</script>
<style lang="scss">
@use './../styles/image_hover.css'
</style>