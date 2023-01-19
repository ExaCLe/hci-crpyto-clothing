<template>
    <v-container>
        <v-row>
            <v-col cols="4">
                <p class="text-h6">{{ item.name }}</p>
            </v-col>
            <v-col cols="4">
                <p class="text-h6 font-weight-bold">{{ item.price }}</p>
            </v-col>
            <v-col cols="4">
                <v-btn variant="plain" @click="$emit('edit')"><v-icon size="30" color="black" icon="mdi-pencil" class="mr-2"/></v-btn>
                <v-btn variant="plain" @click="$emit('delete')"><v-icon size="30" color="black" icon="mdi-trash-can" /></v-btn>
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