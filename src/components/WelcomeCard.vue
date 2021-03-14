<template>
  <ion-content>
    <ion-card>
      <ion-card-header>
        <ion-card-title>Envie de reserver un terrain ?</ion-card-title>
        <ion-card-title>Choississez votre créneau selon les disponibilités.</ion-card-title>
        <ion-card-subtitle>Nous sommes ouverts tout les jours sauf le lundi de 9h à 18h.</ion-card-subtitle>
      </ion-card-header>
      <ion-card-content>
      <a href="/tabs/reservation"><ion-button expand="block">Choisir mon horaire</ion-button></a>
     </ion-card-content>
    </ion-card>
    <ion-card>
      <img src="../assets/img/tennis-municipaux.jpg" alt="">
      <ion-card-header>
        <ion-card-title>Le club vous attends, n'hésitez pas a venir nous voir !</ion-card-title>
        <ion-card-subtitle>Que ce soit pour prendre des cours ou juste jouer, le club est fait pour vous.</ion-card-subtitle>
      </ion-card-header>
    </ion-card>
  </ion-content>
</template>  

<script>
import { IonCard, IonCardContent, IonCardHeader, IonCardSubtitle, IonCardTitle, IonContent, IonButton} from '@ionic/vue';

export default {
  name: 'welcomeCard',
  components: {
    IonCard, 
    IonCardContent, 
    IonCardHeader, 
    IonCardSubtitle, 
    IonCardTitle,
    IonContent,
    IonButton
  }
  
}
</script>
<style scoped>
ion-card-title {
  font-size: 1.5em;
  margin-bottom: 10px;
}

</style>