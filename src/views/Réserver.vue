<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title class="ion-text-center">Réservation</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content>
      <ReservationForm />
    </ion-content>
  </ion-page>
</template>

<script>
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent } from '@ionic/vue';
import ReservationForm from '@/components/ReservationForm.vue';
import { book } from 'ionicons/icons';

export default  {
  name: 'reservation',
  components: { ReservationForm, IonHeader, IonToolbar, IonTitle, IonContent, IonPage },
  setup() {
    return {
      book
    }
  }
}
</script>
<style scoped>
ion-toolbar {
    box-shadow: 0 .125rem .25rem rgba(0,0,0,.075)!important;
}
</style>