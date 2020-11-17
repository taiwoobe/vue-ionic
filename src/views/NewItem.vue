<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-back-button default-href="/"></ion-back-button>
        </ion-buttons>
        <ion-title>New Item</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding">
        <ion-icon :icon="heart"></ion-icon>
        <img :src="photo" alt=""/>
        <ion-button @click="takePhoto()"> Take Photo </ion-button>
    </ion-content>
  </ion-page>
</template>

<script>
import {
  IonBackButton,
  IonButtons,
  IonContent,
  IonHeader,
  IonPage,
  IonTitle,
  IonToolbar
} from '@ionic/vue';
import { heart } from "ionicons/icons";
import { defineComponent, ref } from 'vue';
import { Plugins, CameraResultType } from "@capacitor/core";
const { Camera } = Plugins;

export default defineComponent({
  name: 'NewItem',
  components: {
    IonBackButton,
    IonButtons,
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar
  },
  setup() {
    const imageSrc = ref("");
    const takePhoto = async () => {
      const image = await Camera.getPhoto({
        quality: 90,
        allowEditing: true,
        resultType: CameraResultType.Uri
      });
      imageSrc.value = image.webPath;
    }
    return { heart, photo: imageSrc, takePhoto }
  }
});
</script>