<template>
    <v-container fluid v-if="!showSelectCloth">
        <v-row>
            <v-col cols="3" id="image-container">
                <div id="head-register"></div>
                <div ref="body" @mouseenter="showSpinningWheel" @mouseleave="hideSpinningWheel" 
                    :style="{ boxShadow: displaySpinningWheel ? '0 0 10px 10px red' : 'none' }"
                    id="body-register">
                </div>
                <div id="legs-register"></div> 
                <div id="shoes-register"></div>
                <v-img :src="selectedJacket" id="image"/> 
            </v-col>
            <SpinningWheel :position="spinningWheelPosition" v-if="displaySpinningWheel" v-on:select="updateSelectedJacket"/> 
            <v-col cols="6" id="parts">
                <div id="head">
                    <PurchaseItem v-for="item in items.head" :key="item.id" :item="item"/>
                </div>
                <div id="body">
                    <PurchaseItem v-for="item in items.body" :key="item.id" :item="item"/>
                </div>
                <div id="legs">
                    <PurchaseItem v-for="item in items.legs" :key="item.id" :item="item"/>
                </div>
                <div id="shoes">
                    <PurchaseItem v-for="item in items.shoes" :key="item.id" :item="item"/>
                </div>
            </v-col>
            <v-col align="end" class="row pb-15">
                <v-btn color="primary" class="mt-10">Zur Kasse</v-btn>
                <v-btn color="primary" class="mt-10">Zum Warenkorb</v-btn>
            </v-col>
        </v-row>
    </v-container>
    <v-container fluid v-else>
        <v-row class="row">
            <v-col cols="3" v-for="image in imagesUpper">
                <v-img :src="image" aspect-ratio="1" id="img"/>
            </v-col>
        </v-row>
        <v-row class="row">
            <v-col cols="3" v-for="image in imagesLower">
                <v-img :src="image" aspect-ratio="1" id="img"/>
            </v-col>
        </v-row>
    </v-container>
</template>
<script>
import PurchaseItem from '../components/PurchaseItem.vue'
import SpinningWheel from '../components/SpinningWheel.vue'

export default {
    data() {
        return {
            items: {
                head: [], 
                body: [
                    {
                        name: "Hemd", 
                        price: 89.99, 
                    }, 
                ], 
                legs: [
                    {
                        name: "Premium Jeans", 
                        price: 49.99,
                    }, 
                ],
                shoes: [
                    {
                        name: "Schuhe", 
                        price: 79.99, 
                    }, 
                ],
            }, 
            spinningWheelPosition: {
                x: 0, 
                y: 0, 
            },
            displaySpinningWheel: false,
            showSelectCloth: false, 
            imagesUpper: [
                "/src/assets/Jacket1.png",
                "/src/assets/Jacket2.png",
                "/src/assets/Jacket3.png",
            ], 
            imagesLower: [
                "/src/assets/Jacket4.png",
                "/src/assets/Jacket5.png",
                "/src/assets/Jacket1.png",
            ], 
            selectedJacket: "../src/assets/Men1.png",
        } 
    }, 
    computed: {
        total() {
            return this.items.reduce((total, category) => category.reduce((total, item) => total + item.price, 0), 0)
        }, 
    }, 
    methods: {
        showSpinningWheel(event) {
            const body = this.$refs.body;
            const x = body.offsetWidth / 2 + 20;
            const y = body.offsetHeight + 240;
            this.spinningWheelPosition = { x, y };
            this.displaySpinningWheel = true;
        }, 
        hideSpinningWheel() {
            this.displaySpinningWheel = false;
        },
        updateSelectedJacket(selectedJacket) {
            this.selectedJacket = selectedJacket;
        },
    }, 
    components: {
        PurchaseItem, 
        SpinningWheel,
    }
}
</script>
<style scoped>
.row {
    max-height: 40vh;
}
#image-container {
    display: grid; 
    grid-auto-rows: 2.5%; 
}
#image {
    grid-column: 1;
    grid-row-start: 1;
    grid-row-end: 40; 
    z-index: 0; 
}

#head-register {
    grid-column: 1;
    grid-row-start: 1; 
    grid-row-end: 9; 
    z-index: 100;
    opacity: 0.5;
    background-color: aqua;
}

#body-register {
    grid-column: 1;
    grid-row-start: 9; 
    grid-row-end: 17; 
    z-index: 100;
    opacity: 0.5;
    background-color: red;
}

#legs-register {
    grid-column: 1;
    grid-row-start: 17; 
    grid-row-end: 33; 
    z-index: 100;
    opacity: 0.5;
    background-color: green;
}

#shoes-register {
    grid-column: 1;
    grid-row-start: 33; 
    grid-row-end: 40; 
    z-index: 100;
    opacity: 0.5;
    background-color: blue;
}


.row {
    display: flex; 
    flex-direction: column; 
    justify-content: end; 
}

#head {
    position: relative; 
    top: 0; 
    left: 0; 
    height: 180px;
}

#body {
    position: relative; 
    top: 180; 
    left: 0; 
    height: 150px;
}

#legs {
    position: relative; 
    top: 330; 
    left: 0; 
    height: 350px;
}

#shoes {
    position: relative; 
    top: 680; 
    left: 0; 
    height: 100px;
}
</style>