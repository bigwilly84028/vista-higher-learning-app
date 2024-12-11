<template>
  <ion-page>
    <ion-header :translucent="false">
      <ion-toolbar>
        <ion-title>Learning Material - Section A : Lesson 1</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="false">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Blank</ion-title>
        </ion-toolbar>
      </ion-header>

      <div id="container">
        <ion-grid>
          <ion-row>
            <ion-col></ion-col>
            <ion-col size="10">
              <ion-row>
                <ion-col>
                  <strong>Say the vocabulary words.</strong>
                </ion-col>
              </ion-row>
              <ion-row class="top-spacer-lg">
                <ion-col size="12" size-sm="4">
                  <ion-button shape="round" color="warning" @click="stopfn">
                    <ion-icon slot="icon-only" name="square"></ion-icon>
                  </ion-button>
                  <ion-row>
                    <ion-col>Stop</ion-col>
                  </ion-row>
                </ion-col>
                <ion-col size="12" size-sm="4">
                  <ion-button
                    shape="round"
                    :color="isRecording ? 'success' : 'danger'"
                    @click="recordfn"
                  >
                    <ion-icon slot="icon-only" name="ellipse"></ion-icon>
                  </ion-button>
                  <ion-row>
                    <ion-col>{{
                      isRecording ? "Recording..." : "Record"
                    }}</ion-col>
                  </ion-row>
                </ion-col>
                <ion-col size="12" size-sm="4">
                  <ion-col>
                    <ion-button
                      shape="round"
                      :color="isReviewing ? 'success' : 'primary'"
                      @click="reviewfn"
                    >
                      <ion-icon
                        size="large"
                        slot="icon-only"
                        name="caret-forward"
                      ></ion-icon>
                    </ion-button>
                  </ion-col>
                  <ion-row>
                    <ion-col>{{
                      isReviewing ? "Reviewing..." : "Review your recording"
                    }}</ion-col>
                  </ion-row>
                </ion-col>
              </ion-row>
              <ion-row class="top-spacer-lg">
                <ion-col>
                  <textarea
                    v-model="text"
                    rows="3"
                    cols="20"
                    placeholder="Please submit your answer here..."
                    ref="textArea"
                  >
                  </textarea>
                </ion-col>
              </ion-row>
              <ion-row class="top-spacer-md">
                <ion-col>
                  <p>Is this your final answer?</p>
                </ion-col>
              </ion-row>
              <ion-row class="top-spacer-md">
                <ion-col>
                  <ion-radio-group
                    value="true"
                    @ionChange="handleFinalAnswerChange($event)"
                  >
                    <ion-radio
                      class="margin-right-ten"
                      value="true"
                      aria-label="Custom checkbox that is checked"
                      >No</ion-radio
                    >
                    <ion-radio value="false" aria-label="Custom checkbox"
                      >Yes</ion-radio
                    >
                  </ion-radio-group>
                </ion-col>
              </ion-row>
              <ion-row class="top-spacer-md">
                <ion-col>
                  <button
                    class="submit-button"
                    :disabled="submitDisabled"
                    @click="submitfn"
                  >
                    Submit
                  </button>
                </ion-col>
              </ion-row>
            </ion-col>
            <ion-col></ion-col>
          </ion-row>
        </ion-grid>
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
  IonTextarea,
  IonRadio,
  IonRadioGroup,
} from "@ionic/vue";
import { square, ellipse, caretForward } from "ionicons/icons";
import { addIcons } from "ionicons";
import { ref } from "vue";

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
    IonTextarea,
    IonRadio,
    IonRadioGroup,
  },
  created: function () {
    addIcons({
      square: square,
      ellipse: ellipse,
      "caret-forward": caretForward,
    });
  },
  setup() {
    const textArea = ref(null);
    const isRecording = ref(false);
    const isReviewing = ref(false);
    const submitDisabled = ref(true);

    const stopfn = () => {
      // should focus text area only if recording is already in progress?
      // or also if reviewing is in process as well?
      if (isRecording.value == true || isReviewing.value == true) {
        if (textArea.value) {
          textArea.value.focus();
        }
      }

      isRecording.value = false;
      isReviewing.value = false;
    };

    const recordfn = () => {
      isRecording.value = true;
      isReviewing.value = false;
    };

    const reviewfn = () => {
      isRecording.value = false;
      isReviewing.value = true;
    };

    const submitfn = () => {
      alert("You answers have been submitted!");
    };

    const handleFinalAnswerChange = (ev) => {
      console.log("Current value:", ev.detail.value);
      // Small issue with string event value vs boolean vals:
      submitDisabled.value = ev.detail.value === "true";
    };

    return {
      square,
      ellipse,
      caretForward,
      handleFinalAnswerChange,
      submitDisabled,
      isRecording,
      isReviewing,
      stopfn,
      recordfn,
      reviewfn,
      textArea,
      submitfn,
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

ion-radio::part(container) {
  width: 30px;
  height: 30px;

  border-radius: 8px;
  border: 2px solid #ddd;
}

ion-radio::part(mark) {
  background: none;
  transition: none;
  transform: none;
  border-radius: 0;
}

ion-radio.radio-checked::part(container) {
  background: #2dd55b;
  border-color: transparent;
}

ion-radio.radio-checked::part(mark) {
  width: 6px;
  height: 10px;

  border-width: 0px 2px 2px 0px;
  border-style: solid;
  border-color: #fff;

  transform: rotate(45deg);
}

/* Button Style */

.submit-button {
  background-color: #5f98ff;
  width: 100%;
  padding: 15px;
  font-size: 17px;
  font-weight: bold;
  color: #fff;
  text-transform: uppercase;
  border-radius: 28px;
  cursor: pointer;
}

.submit-button:disabled {
  background-color: #d9d9d9;
  color: #898989;
}

.submit-button:focus {
  border: 0.75em solid rgb(255, 200, 0);
}

.submit-button:hover {
  background-color: #3872dd;
}

.top-spacer-md {
  padding-top: 35px;
}

.top-spacer-lg {
  padding-top: 50px;
}

.margin-right-ten {
  margin-right: 30px;
}

textarea {
  padding: 10px;
  width: 100%;
}
</style>
