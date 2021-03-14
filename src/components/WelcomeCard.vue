<template>
  <ion-content>
    <ion-card>
      <ion-card-header>
        <ion-card-subtitle>Destination</ion-card-subtitle>
        <ion-card-title>Madison, WI</ion-card-title>
      </ion-card-header>
      <ion-card-content>
        Founded in 1829 on an isthmus between Lake Monona and Lake Mendota, Madison was named the capital of the Wisconsin Territory in 1836.
      </ion-card-content>
    </ion-card>
  </ion-content>
</template>

<script>
import { IonCard, IonCardContent, IonCardHeader, IonCardSubtitle, IonCardTitle} from '@ionic/vue';

export default {
  name: 'welcomeCard',
  components: {
    IonCard, 
    IonCardContent, 
    IonCardHeader, 
    IonCardSubtitle, 
    IonCardTitle
  }
  
}
</script>

<style lang="scss" scoped>

</style>