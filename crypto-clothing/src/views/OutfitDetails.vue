<template>
    <v-container fluid>
        <v-row>
            <v-col cols="3" id="image-container">
                <div id="head-register"></div>
                <div id="body-register"></div>
                <div id="legs-register"></div>
                <div id="shoes-register"></div>
                <v-img src="../assets/Men1.png" id="image"/> 
            </v-col>
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
</template>
<script>
import PurchaseItem from '../components/PurchaseItem.vue'

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
            }
        } 
    }, 
    computed: {
        total() {
            return this.items.reduce((total, category) => category.reduce((total, item) => total + item.price, 0), 0)
        }, 
    }, 
    components: {
        PurchaseItem
    }
}
</script>
<style>
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