<template>
    <ion-button color="light" expand="block" v-if="info" @click="$emit('clear-info')">
        <ion-icon ios="ios-trash" md="md-trash"></ion-icon>
    </ion-button>
</template>

<script>
    export default {
        name: "ClearInfo",
        props: ["info"]

    }
</script>