<template>
    <ion-card id="card">
      <ion-card-header>
        <div v-if="validationMessage">
          <ion-text color="success">
             <h2>
               {{ validationMessage ? validationMessage : cancelVerified }}.
            </h2>
          </ion-text><br>
          <ion-text>
            <div>Je ne suis plus disponible a cette date :</div>
            <div>
              <ion-button @click="cancelReservation" expand="block">Annuler ma réservation</ion-button>
            </div>
          </ion-text><br>
          <ion-text v-if="cancelVerified" color="success">
            <h2>
              Votre réservation a bien été annulée.
            </h2>
          </ion-text>
        </div>
        <ion-card-title>Je réserve mon terrain pour une heure.</ion-card-title>  
        <ion-card-subtitle>2 places/heures disponibles.</ion-card-subtitle>
        <ion-card-subtitle>Seulement en heure complète (exemple: 17h00).</ion-card-subtitle>
        <ion-text v-for="error in errors" :key="error" color="danger">
          <h2>
            {{error}}
          </h2>
        </ion-text>
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
          <ion-label>Conditions d'utilisation</ion-label>
          <ion-checkbox v-model="cgu" color="primary" slot="start"></ion-checkbox>
        </ion-item>
      <section>
        <ion-button id="reserve" expand="block" @click="sendReservation">réserver</ion-button>
      </section>
      </ion-card-content>
    </ion-card>
</template>

<script>
import axios from 'axios';
// import CancelConfirmation from '@/components/CancelConfirmation';
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
  },
  data(){
    return {  
      email: "",
      selectedDate: "",
      cgu: false,
      errors: [],
      validationMessage: "",
      token: "",
      cancelVerified: false,
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
    this.errors = []
    },
    cancelReservation(){
      axios(`https://tennis-affluence.herokuapp.com/api/reservation/annulation/${this.token}`, {
          method: 'POST',
          headers: {
          'Accept': 'application/json',
          'Content-Type': 'application/json'
        }
      })
      .then((response)=> {
        if(response.status === 204) return this.cancelVerified = true
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
  --background: #D97706;
}
#reserve {
  margin-top: 2rem; 
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