<template>
    <ion-page ref="page">
        <ion-header>
            <ion-toolbar>
                <ion-buttons slot="end">
                    <ion-button v-if="isModal" @click="closeModal()">Close</ion-button>
                </ion-buttons>
                <ion-title>Hello World</ion-title>
            </ion-toolbar>
        </ion-header>
        <ion-content class="ion-padding">
            <p>This is a page.</p>
            <ion-button @click="openInModal()">Open this page in modal</ion-button>
        </ion-content>
    </ion-page>
</template>

<script lang="ts">
import { defineComponent, defineAsyncComponent, ref, onMounted } from 'vue';
import { IonPage, IonButtons, IonButton, IonHeader, IonToolbar, IonTitle, IonContent, modalController } from '@ionic/vue';

export default defineComponent({
    name: 'HelloWorld',
    components: {
        IonPage,
        IonButtons,
        IonButton,
        IonHeader,
        IonToolbar,
        IonTitle,
        IonContent
    },
    props: {
        msg: String
    },
    setup() {
        const page = ref<typeof IonPage>();
        const isModal = ref<boolean>(false);

        onMounted(() => {
            if (page.value) {
                isModal.value = !!page.value.$el.closest('ion-modal');
            }
        });

        async function openInModal() {
            const modal = await modalController.create({
                component: defineAsyncComponent(() => import('./HelloWorld.vue'))
            });
            modal.present();
        }

        async function closeModal() {
            modalController.dismiss();
        }

        return {
            page,
            isModal,
            closeModal,
            openInModal
        };
    }
});
</script>
