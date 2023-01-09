<template> 
<div >
    <v-avatar :size="avatarSize" v-for="card in cards" :style='{left: card.left + "px", top: card.top + "px"}' class="card">
        <img :src="card.path" />
    </v-avatar>
</div>
</template>
<script>
export default {
    data() {
        return {
            avatarSize: 64, 
            cards: [
                {
                    path: "/src/assets/Jacket1.png",
                    left: 0,
                    top: 0,
                }, 
                {
                    path: "/src/assets/Jacket2.png",
                    left: 0,
                    top: 0,
                }, 
                {
                    path: "/src/assets/Jacket3.png",
                    left: 0, 
                    top: 0,
                }, 
                {
                    path: "/src/assets/Jacket4.png",
                    left: 0, 
                    top: 0, 
                }, 
                {
                    path: "/src/assets/Jacket5.png",
                    left: 0,
                    top: 0,
                }, 
            ]
        }
    }, 
    mounted() {
        this.positionCards();
    },
    props: {
        position: {
            type: Object, 
            required: true,
        }, 
    }, 
    watch: {
        position: {
            handler() {
                this.positionCards(); 
            }, 
            deep: true, 
        }, 
    }, 
    methods: {
        positionCards() {
            const wheelRadius = 100; 
            const center = {
                x: this.position.x, 
                y: this.position.y// this.cards[0].top,
            }

            this.cards.forEach((card, index) => {
                const theta = 2 * Math.PI / this.cards.length * index; 
                const x = Math.cos(theta) * wheelRadius; 
                const y = -1.0 * Math.sin(theta) * wheelRadius;
                const middle = {
                    x: this.avatarSize / 2,
                    y: this.avatarSize / 2,
                }

                card.left = center.x + x - middle.x;
                card.top = center.y + y - middle.y;
            })
        }
    }
}
</script>
<style scoped>
.card {
    position: absolute;
    z-index: 1000;
    opacity: 1;
}

.wheel {
    position: absolute;
    top: 50%; 
    left: 50%;

    transform: translate(-50%, -50%);

    width: 200px;
    background-color: green;
    height: 200px; 
}
</style>