<template>
    <v-container>
        <v-row align="center" justify="center" class="mt-15">
            <v-badge color="red" content="4">
                <v-icon class="pa-10 icon" size="100">mdi-cart-outline</v-icon>
            </v-badge>
            <p class="text-lg-h1 pa-10 mr-30">Artikel zum Warenkorb hinzgefügt.</p>
        </v-row>
        <v-row align="center" justify="center" class="mt-10">
            <v-btn color="primary" class="mt-10 mx-10" @click="this.$router.push('/cart')" height="80"><p class="text-lg-h4">Zur Kasse</p></v-btn>
        </v-row>
        <v-row align="center" justify="center" class="mt-10">
            <v-btn color="primary" height="80" outlined class="mt-10" @click="this.$router.push('/outfits')"><p class="text-lg-h5">Neues Outfit</p></v-btn>
        </v-row>
    </v-container>
</template>