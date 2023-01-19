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
                {icon: 'mdi-gender-male', label: 'Männlich'},
                {icon: 'mdi-gender-female', label: 'Weiblich'}, 
            ], 
            sex: undefined, 
            environmentOptions: [
                {icon: 'mdi-home', label: 'Drinnen'}, 
                {icon: 'mdi-nature', label: 'Draußen'}, 
            ], 
            environment: undefined,
            heatOptions: [
                {icon: 'mdi-weather-sunny', label: 'Sommer'}, 
                {icon: 'mdi-weather-cloudy', label: 'Herbst'},
                {icon: 'mdi-weather-snowy', label: 'Winter'},
            ],
            heat: undefined,
            occasionOptions: [
                {icon: 'party-popper', label: 'Feier'}, 
                {icon: 'mdi-sofa', label: 'Zuhause'}, 
                {icon: 'mdi-briefcase', label: 'Arbeit'}, 
                {icon: 'mdi-ferris-wheel', label: 'Freizeit'},
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