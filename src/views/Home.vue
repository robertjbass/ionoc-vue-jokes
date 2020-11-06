<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Jokes</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Blank</ion-title>
        </ion-toolbar>
      </ion-header>
      <div id="container">
        <br>
        <div class="twoPart" v-if="jokes.type == 'twopart'">
          <br><br>
          <strong>{{jokes.setup}}</strong><br>
          <strong>{{jokes.delivery}}</strong>
        </div>
        <div v-else class="singlePart">
          <strong>{{jokes.joke}}</strong>
        </div>
        <br>
        <ion-button color="dark" @click="this.getJokes">New Joke</ion-button>
      </div>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar } from '@ionic/vue';
import { defineComponent } from 'vue';
import * as math from 'mathjs'
import axios from 'axios';

export default defineComponent({
  name: 'Home',
  data() {
    return {
      jokes: [],
      category: "",
      categoryCount: 0,
      url: "",
    }
  },
  mounted () {
    this.getJokes()
  },
  methods: {
    getJokes() {
    this.categoryCount = math.randomInt(0,5)
    this.url = `https://sv443.net/jokeapi/v2/joke/${['Miscellaneous', 'Programming', 'Dark', 'Pun', 'Spooky', 'Christmas'][this.categoryCount]}`
    axios.get(this.url)
    .then(res => {
      this.jokes = res.data
    })
    .catch(err => {
      console.error(err); 
    });
    }
  },
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar
  }
});
</script>

<style scoped>
#container {
  text-align: center;
  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
  padding: 0 40px
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;
  color: #8c8c8c;
  margin: 0;
}

#container a {
  text-decoration: none;
}
</style>