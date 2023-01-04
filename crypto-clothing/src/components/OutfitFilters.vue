<template>
    <v-container v-if="show">
        <FilterOption v-model="sex" :options="sexOptions" label="Geschlecht:"/>
        <FilterOption v-model="environment" :options="environmentOptions" label="Umgebung:"/>
        <FilterOption v-model="heat" :options="heatOptions" label="Wärme:"/>
        <FilterOption v-model="occasion" :options="occasionOptions" label="Anlass:"/>
        <v-row justify="end"><v-btn color="primary" @click="show = false">Weiter</v-btn></v-row>
    </v-container>
</template>
<script>
import FilterOption from '../components/FilterOption.vue'

export default {
    components: {
        FilterOption
    }, 
    props: {
        modelValue: {
            type: Boolean,
            default: true, 
            required: true, 
        }
    }, 
    data() {
        return {
            sexOptions: [
                'mdi-gender-male', 
                'mdi-gender-female', 
            ], 
            sex: undefined, 
            environmentOptions: [
                'mdi-home', 
                'mdi-nature', 
            ], 
            environment: undefined,
            heatOptions: [
                'mdi-weather-sunny', 
                'mdi-weather-windy', 
                'mdi-weather-snowy', 
            ],
            heat: undefined,
            occasionOptions: [
                'mdi-party-popper', 
                'mdi-sofa', 
                'mdi-briefcase', 
                'mdi-ferris-wheel', 
            ], 
            occasion: undefined,
        }
    }, 
    computed: {
        show: {
            get() {
                return this.modelValue
            }, 
            set(value) {
                this.$emit('update:modelValue', value)
            }
        }
    }
}
</script>