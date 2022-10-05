<template>
    <v-card elevation="10" class="d-flex align-center">
        <v-col cols="1">
            <v-btn icon @click="$emit('status')">
                <v-icon v-if="product.active" color="purple">mdi-check-all</v-icon>
                <v-icon v-else>mdi-checkbox-blank-circle-outline</v-icon>
            </v-btn>
        </v-col>
        <v-col>
            <v-card-text>{{product.name}}</v-card-text>
        </v-col>
        <v-col cols="2">
            <v-btn @click="$emit('delete')" icon>
                <v-icon>mdi-close-circle-outline</v-icon>
            </v-btn>
        </v-col>
    </v-card>
</template>

<script>
export default {
    name: 'CardProductPage',
    props: ['product'],
    data() {
        return {
        }
    },
    computed: {
    },
    methods: {
    }
}
</script>

<style>

</style>