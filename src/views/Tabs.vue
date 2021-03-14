<template>
  <ion-page>
    <ion-tabs>
      <ion-tab-bar slot="bottom">
        <ion-tab-button tab="tab1" href="/tabs/accueil">
          <ion-icon :icon="tennisball" />
          <ion-label>Accueil</ion-label>
        </ion-tab-button>    
        <ion-tab-button tab="tab2" href="/tabs/reservation">
          <ion-icon :icon="book"></ion-icon>
          <ion-label>Réserver</ion-label>
        </ion-tab-button>
      </ion-tab-bar>
    </ion-tabs>
  </ion-page>
</template>

<script>
import { IonTabBar, IonTabButton, IonTabs, IonLabel, IonIcon, IonPage } from '@ionic/vue';
import { tennisball, book } from 'ionicons/icons';

export default {
  name: 'Tabs',
  components: { IonLabel, IonTabs, IonTabBar, IonTabButton, IonIcon, IonPage },
  setup() {
    return {
      tennisball,
      book
    }
  }
}
</script>
<style scoped>
ion-tab-bar{
    --color-selected: #D97706 !important;
}
</style>