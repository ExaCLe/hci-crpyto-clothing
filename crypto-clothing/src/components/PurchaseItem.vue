<template>
    <v-container>
        <v-row>
            <v-col cols="8">
                <p class="text-h6">{{ item.name }}</p>
            </v-col>
            <v-col cols="4">
                <p class="text-h6 font-weight-bold">{{ item.price }}</p>
            </v-col>
        </v-row>
    </v-container>
</template>
<script>
export default {
    props: {
        item: Object, 
    }
}
</script>