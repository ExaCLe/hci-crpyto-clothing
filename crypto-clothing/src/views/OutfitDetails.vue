<template>
    <v-container fluid v-if="!showSelectCloth">
        <v-btn color="primary" variant="outlined" class="mb-2">← Back</v-btn>
        <v-row>
            <v-col cols="3" id="image-container">
                <div id="head-register"></div>
                <div ref="body" @click="positionSpinningWheel"
                    :style="{ boxShadow: displaySpinningWheel ? '0 0 10px 10px red' : 'none' }"
                    id="body-register">
                </div>
                <div id="legs-register"></div> 
                <div id="shoes-register"></div>
                <v-img :src="selectedJacket" id="image"/> 
            </v-col>
            <v-overlay v-model="overlay" persistent>
                <div class="highlight d-flex align-center justify-center" @click="hideOverlayAndOpenSpinningWheel"> 
                    <p :style="{color: 'white', fontSize: '30px'}">Click here to add a new item</p>
                </div>
            </v-overlay>
            <SpinningWheel :position="spinningWheelPosition" v-if="displaySpinningWheel" v-on:select="updateSelectedJacket"/> 
            <v-col cols="6" id="parts">
                <div id="head">
                    <PurchaseItem v-for="item in items.head" :key="item.id" :item="item" @edit="showSelectCloth = true;" @delete="removeItem(item)"/>
                </div>
                <div id="body">
                    <PurchaseItem v-for="item in items.body" :key="item.id" :item="item" @edit="showSelectCloth = true;" @delete="removeItem(item)"/>
                </div>
                <div id="legs">
                    <PurchaseItem v-for="item in items.legs" :key="item.id" :item="item" @edit="showSelectCloth = true;" @delete="removeItem(item)"/>
                </div>
                <div id="shoes">
                    <PurchaseItem v-for="item in items.shoes" :key="item.id" :item="item" @edit="showSelectCloth = true;" @delete="removeItem(item)"/>
                </div>
            </v-col>
            <v-col align="end" class="row pb-15">
                <p class="text-lg-h4">{{ total + ' €' }}</p>
                <v-btn color="primary" class="mt-10" variant="outlined">Zur Kasse</v-btn>
                <v-btn color="primary" class="mt-5" @click="this.$router.push('/cart')">Zum Warenkorb</v-btn>
            </v-col>
        </v-row>
    </v-container>
    <v-container fluid v-else>
        <v-row class="item">
            <v-col cols="3" v-for="item in imagesUpper">
                <v-card>
                    <v-img :src="item.path" aspect-ratio="1" id="img" :style="{maxHeight: '30vh'}"/>
                    <v-row>
                        <v-col align="end" class="mt-5">
                            <p class="text-lg-h4">{{ item.price + ' €' }}</p>
                        </v-col>
                    </v-row>
                    <v-row> 
                        <v-col align="end" class="my-5">
                            <v-btn class="mx-5" color="primary" variant="outlined" >Details</v-btn>
                            <v-btn class="mx-5" color="primary" @click="showSelectCloth=false">Auswählen</v-btn>
                        </v-col>
                    </v-row>
                </v-card>
            </v-col>
        </v-row>
        <v-row class="item">
            <v-col cols="3" v-for="item in imagesLower">
                <v-card>
                    <v-img :src="item.path" aspect-ratio="1" id="img" :style="{maxHeight: '30vh'}"/>
                    <v-row>
                        <v-col align="end" class="mt-5">
                            <p class="text-lg-h4">{{ item.price + ' €' }}</p>
                        </v-col>
                    </v-row>
                    <v-row> 
                        <v-col align="end" class="my-5">
                            <v-btn class="mx-5" color="primary" variant="outlined" >Details</v-btn>
                            <v-btn class="mx-5" color="primary">Auswählen</v-btn>
                        </v-col>
                    </v-row>
                </v-card>
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
            overlay: true,  
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
                {
                    path: "/src/assets/Jacket1.png",
                    price: 119.99,
                }, 
                {
                    path: "/src/assets/Jacket2.png",
                    price: 104.99, 
                }, 
                {
                    path: "/src/assets/Jacket3.png",
                    price: 84.99, 
                }, 
            ], 
            imagesLower: [
                {
                    path: "/src/assets/Jacket4.png",
                    price: 84.99, 
                }, 
                {
                    path: "/src/assets/Jacket5.png",
                    price: 69.99,
                }, 
                {
                    path: "/src/assets/Jacket1.png",
                    price: 74.99, 
                },
            ], 
            selectedJacket: "../src/assets/Men1.png",
        } 
    }, 
    computed: {
        total() {
            let total = 0; 
            Object.keys(this.items).forEach((category) =>  {
                total += this.items[category].reduce((total, item) => total + item.price, 0); 
            })
            return total.toFixed(2)
        }, 
    }, 
    methods: {
        hideSpinningWheel() {
            this.displaySpinningWheel = false;
        },
        removeItem(item) {
            this.items.body = this.items.body.filter((i) => i.name !== item.name);
            this.selectedJacket = "../src/assets/Men1.png";
        },
        updateSelectedJacket(selectedJacket) {
            if (this.items.body.filter((item) => item.name === "Sakko").length > 0) return;
            this.selectedJacket = selectedJacket;
            this.showSelectCloth = true; 
            this.displaySpinningWheel = false;
            this.items.body.push({
                name: "Sakko", 
                price: 104.99, 
            });
        },
        positionSpinningWheel(event) {
            this.spinningWheelPosition = { x: event.clientX, y: event.clientY };
            this.displaySpinningWheel = true;
        }, 
        hideOverlayAndOpenSpinningWheel(event) {
            this.overlay = false; 
            this.positionSpinningWheel(event);
        },
    }, 
    components: {
        PurchaseItem, 
        SpinningWheel,
    }
}
</script>
<style scoped>
.highlight {
    background-color: red;
    opacity: 0.5;
    height: 300px;
    width: 705px; 
    position: absolute;
    top: 500px; 
    left: 25px; 

}

.item {
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
    /* background-color: aqua; */
}

#body-register {
    grid-column: 1;
    grid-row-start: 9; 
    grid-row-end: 17; 
    z-index: 100;
    opacity: 0.5;
    /* background-color: red; */
}

#legs-register {
    grid-column: 1;
    grid-row-start: 17; 
    grid-row-end: 33; 
    z-index: 100;
    opacity: 0.5;
    /* background-color: green; */
}

#shoes-register {
    grid-column: 1;
    grid-row-start: 33; 
    grid-row-end: 40; 
    z-index: 100;
    opacity: 0.5;
    /* background-color: blue; */
}


.row {
    display: flex; 
    flex-direction: column; 
    justify-content: end; 
    max-height: 80vh;
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