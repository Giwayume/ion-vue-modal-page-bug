<template>
    <ion-app>
        <HelloWorld msg="Welcome to Your Vue.js + TypeScript App"/>
    </ion-app>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { IonApp } from '@ionic/vue';
import HelloWorld from './components/HelloWorld.vue';

export default defineComponent({
    name: 'App',
    components: {
        IonApp,
        HelloWorld
    }
});
</script>
