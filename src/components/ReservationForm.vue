<template>
    <ion-card id="card">
      <ion-card-header>
        <div  v-if="validationMessage">
          <ion-text> {{ validationMessage }}</ion-text>
          <a :href="'/reservation/annulation/' + token"> Annuler la réservation</a>
          <cancel-confirmation />
        </div>
        <ion-card-title>Je réserve mon terrain pour une heure.</ion-card-title>  
        <ion-card-subtitle>2 places/heures disponibles.</ion-card-subtitle>
        <ion-card-subtitle>Seulement en heure complète (exemple: 17h00).</ion-card-subtitle>
        <ion-text v-for="error in errors" :key="error"> {{error}} </ion-text>
      </ion-card-header>
      <ion-card-content>
        <ion-item>
          <ion-label>Choisir une date:</ion-label>
          <ion-datetime v-model="selectedDate" minute-values="00" cancel-text="annuler" done-text="valider" placeholder="Choisir une date" display-format="YYYY-MM-DD HH:mm"  picker-format="YYYY-MM-DDTHH:mm"></ion-datetime>
        </ion-item>
        <ion-item>
          <ion-label>Adresse e-mail:</ion-label>
          <ion-input v-model="email" placeholder="email"></ion-input>
      </ion-item>
        <ion-item>
          <ion-label>Accepter les conditions d'utilisation</ion-label>
          <ion-checkbox v-model="cgu" color="primary" slot="start"></ion-checkbox>
        </ion-item>
      <section>
        <ion-button expand="block" @click="sendReservation">réserver</ion-button>
      </section>
      </ion-card-content>
    </ion-card>
</template>

<script>
import axios from 'axios';
import CancelConfirmation from '@/components/CancelConfirmation';
import { IonCard, IonCardContent, IonCardHeader, IonItem, IonLabel, IonDatetime, IonCardSubtitle, IonCardTitle, IonCheckbox, IonInput, IonButton, IonText } from '@ionic/vue';

export default  {
  name: 'reservationForm',
  components: {  
    IonCard,
    IonCardContent, 
    IonCardHeader, 
    IonItem, 
    IonLabel, 
    IonDatetime, 
    IonCardSubtitle, 
    IonCardTitle, 
    IonCheckbox,
    IonInput,
    IonButton,
    IonText,
    CancelConfirmation
  },
  data(){
    return {  
      email: "",
      selectedDate: "",
      cgu: false,
      errors: [],
      validationMessage: "",
      token: "",
    }
  },
  methods:{
    sendReservation(){
      axios("https://tennis-affluence.herokuapp.com/api/reservation", {
          method: 'POST',
          headers: {
          'Accept': 'application/json',
          'Content-Type': 'application/json'
        },
        data: {
          email: this.email,
          date: this.selectedDate.substring(0, 16),
          cgu: this.cgu
        } 
      })
      .then((response)=> {
        if(response.status === 201) return this.validationMessage = response.data.message, this.token = response.data.token
        console.log(response)
      })
      .catch(error => {
        if(error.response.status === 400 || error.response.status ===  422){
          return this.errors.push(error.response.data.messages[0])
          }
          console.log(error.response.data);
          console.log(error.response.status);
          console.log(error.response.headers);
    });
    },
  }
}
</script>
<style scoped>
ion-button {
  margin-top: 2rem;
  --background: #D97706;
}
#card {
  padding: 1rem;
  margin-top: 6em;
}
ion-card-subtitle {
  margin: 10px 5px;
}
ion-card-content {
  padding: 0 5px 5px;
}
</style>