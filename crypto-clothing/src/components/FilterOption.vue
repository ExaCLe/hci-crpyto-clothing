<template>
    <v-row align="center" justify="start">
        <v-col cols="12" sm="6" md="4" lg="3" class="text-lg-h4">
            {{ label }}
        </v-col>
        <v-spacer/>
        <v-col cols="10" sm="5" md="4" lg="2" v-for="option, index in options" align="end">
            <v-icon size="60" :color="selectedIndex == index ? 'blue': undefined" @click="selectIndex(index)" :icon="option.icon"/>
            <p class="text-h5" :style="{color: selectedIndex == index ? '#2196f3' : 'black'}">{{ option.label }}</p>
        </v-col>
    </v-row>
    <v-icon size="70">mdi-female</v-icon> 
</template>
<script>
export default {
    props: {
        modelValue: {
            default: undefined, 
            required: true, 
        }, 
        options: {
            type: Array,
            default: () => [], 
            required: true, 
        }, 
        label: {
            type: String, 
            default: undefined, 
            required: true, 
        }
    }, 
    computed: {
        selectedIndex: {
            get() {
                return this.modelValue
            },
            set(value) {
                this.$emit('update:modelValue', value)
            }
        }, 
    }, 
    methods: {
        selectIndex(index) {
            this.selectedIndex = index
        },
    }
}
</script>