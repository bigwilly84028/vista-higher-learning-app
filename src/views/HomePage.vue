<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Blank</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Blank</ion-title>
        </ion-toolbar>
      </ion-header>

      <div id="container">
        <strong>Say the vocabulary words.</strong>
        <ion-grid>
          <ion-row>
            <ion-col>
              <ion-button shape="round" color="warning">
                <ion-icon slot="icon-only" name="square"></ion-icon>
              </ion-button>
            </ion-col>
            <ion-col>
              <ion-button shape="round" color="danger">
                <ion-icon slot="icon-only" name="ellipse"></ion-icon>
              </ion-button>
            </ion-col>
            <ion-col>
              <ion-button shape="round" color="primary">
                <ion-icon slot="icon-only" name="caret-forward"></ion-icon>
              </ion-button>
            </ion-col>
          </ion-row>
        </ion-grid>
        <!-- <p>
          Start with Ionic
          <a
            target="_blank"
            rel="noopener noreferrer"
            href="https://ionicframework.com/docs/components"
            >UI Components</a
          >
        </p> -->
      </div>
    </ion-content>
  </ion-page>
</template>

<script>
import {
  IonContent,
  IonHeader,
  IonPage,
  IonTitle,
  IonToolbar,
  IonGrid,
  IonRow,
  IonCol,
  IonButton,
  IonIcon,
} from "@ionic/vue";
import { square, ellipse, caretForward } from "ionicons/icons";
import { addIcons } from "ionicons";

export default {
  name: "HomePage",
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    IonGrid,
    IonRow,
    IonCol,
    IonButton,
    IonIcon,
  },
  created: function () {
    addIcons({
      square: square,
      ellipse: ellipse,
      "caret-forward": caretForward,
    });
  },
  setup() {
    //const state = "athing";

    return {
      square,
      ellipse,
      caretForward,
    };
  },
};
</script>

<style scoped>
#container {
  text-align: center;

  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
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
