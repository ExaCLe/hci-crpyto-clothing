<template> 
<div>
    <div  v-for="card in cards" class="card" :style='{left: card.left + "px", top: card.top + "px"}'>
        <v-avatar :size="avatarSize" @click="selectJacket" class="avatar">
            <img :src="card.path" style="transform: scale(0.1);"/>
        </v-avatar>
        <p :style="{color: 'white'}" class="text-lg-h6">{{ card.text }}</p>
    </div>
</div>
</template>
<script>
export default {
    data() {
        return {
            avatarSize: 92, 
            cards: [
                {
                    path: "/src/assets/Jacket1.png",
                    left: 0,
                    top: 0,
                    text: "Jacken", 
                }, 
                {
                    path: "/src/assets/Jacket2.png",
                    left: 0,
                    top: 0,
                    text: "Sakkos", 
                }, 
                {
                    path: "/src/assets/Jacket3.png",
                    left: 0, 
                    top: 0,
                    text: "Mäntel", 
                }, 
                {
                    path: "/src/assets/Jacket4.png",
                    left: 0, 
                    top: 0, 
                    text: "Hemden"
                }, 
                {
                    path: "/src/assets/Jacket5.png",
                    left: 0,
                    top: 0,
                    text: "T-Shirs",
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
            const wheelRadius = 130; 
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
        },
        selectJacket() {
            this.$emit("select", "/src/assets/MenWithJacket.png");
        }
    }
}
</script>
<style scoped>
.card {
    position: absolute;
    z-index: 1000;
    opacity: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
}

.avatar {
    box-shadow: 0 0 7px 7px rgb(243, 89, 89);
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