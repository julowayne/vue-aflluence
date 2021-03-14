<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title  class="ion-text-center">Accueil</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <welcome-card />
      <google-map />
    </ion-content>
  </ion-page>
</template>

<script>
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent } from '@ionic/vue';
import GoogleMap from '@/components/GoogleMap.vue';
import WelcomeCard from '@/components/WelcomeCard.vue';
import { tennisball } from 'ionicons/icons';

export default  {
  name: 'Accueil',
  components: {GoogleMap, WelcomeCard,  IonHeader, IonToolbar, IonTitle, IonContent, IonPage },
    setup() {
    return {
      tennisball
    }
  }
}
</script>
<style scoped>
ion-icon {
  margin-top: 5px;
}
ion-title {
  box-shadow: 0 .125rem .25rem rgba(0,0,0,.075)!important;
}
ion-toolbar {
    box-shadow: 0 .125rem .25rem rgba(0,0,0,.075)!important;
}
</style>