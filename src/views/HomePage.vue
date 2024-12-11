<template>
  <ion-page>
    <ion-header :translucent="false">
      <ion-toolbar>
        <ion-title>Learning Material - Section A : Lesson 1</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="false" role="main">
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
                  <h2>Say the vocabulary words.</h2>
                </ion-col>
              </ion-row>
              <ion-row
                class="top-spacer-lg"
                aria-labelledby="recording-controls"
              >
                <ion-col size="12" size-sm="4">
                  <ion-button
                    shape="round"
                    color="warning"
                    @click="stopfn"
                    aria-label="Stop recording"
                    aria-disabled="!isRecording && !isReviewing"
                  >
                    <ion-icon
                      slot="icon-only"
                      name="square"
                      alt="Stop"
                    ></ion-icon>
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
                    :aria-pressed="isRecording"
                    aria-label="Toggle recording"
                  >
                    <ion-icon
                      slot="icon-only"
                      name="ellipse"
                      alt="Record"
                    ></ion-icon>
                  </ion-button>
                  <ion-row>
                    <ion-col aria-live="polite">{{
                      isRecording ? "Recording..." : "Record"
                    }}</ion-col>
                  </ion-row>
                </ion-col>
                <ion-col size="12" size-sm="4">
                  <ion-button
                    shape="round"
                    :color="isReviewing ? 'success' : 'primary'"
                    @click="reviewfn"
                    :aria-pressed="isReviewing"
                    aria-label="Toggle review recording"
                  >
                    <ion-icon
                      slot="icon-only"
                      name="caret-forward"
                      alt="Review"
                    ></ion-icon>
                  </ion-button>
                  <ion-row>
                    <ion-col aria-live="polite">{{
                      isReviewing ? "Reviewing..." : "Review your recording"
                    }}</ion-col>
                  </ion-row>
                </ion-col>
              </ion-row>
              <ion-row class="top-spacer-lg">
                <ion-col class="text-left">
                  <label for="text-area">
                    Comments <span class="required-text">(Required)</span>
                  </label>
                  <textarea
                    id="text-area"
                    v-model="text"
                    rows="3"
                    cols="20"
                    placeholder="Please submit your answer here..."
                    ref="textArea"
                    aria-required="true"
                    class="margin-top-five"
                  ></textarea>
                </ion-col>
              </ion-row>
              <ion-row class="top-spacer-md ion-align-items-center">
                <ion-col size="auto" class="text-right">
                  <span
                    id="final-answer-question"
                    class="pad-right-ten text-bold"
                    >Is this your final answer?
                  </span>
                </ion-col>
                <ion-col size="auto" class="text-left">
                  <ion-radio-group
                    aria-labelledby="final-answer-question"
                    @ionChange="handleFinalAnswerChange($event)"
                  >
                    <ion-radio
                      class="margin-right-ten"
                      value="true"
                      aria-label="No, not my final answer"
                    >
                      No
                    </ion-radio>
                    <ion-radio
                      value="false"
                      aria-label="Yes, this is my final answer"
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
                    aria-disabled="submitDisabled"
                    aria-label="Submit final answer"
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

#container a {
  text-decoration: none;
}

/* Radio button Styles */

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

/* Textarea Style */

textarea {
  padding: 10px;
  width: 100%;
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

/* Reusable Utility Styles */

.top-spacer-md {
  padding-top: 35px;
}

.top-spacer-lg {
  padding-top: 50px;
}

.margin-right-ten {
  margin-right: 30px;
}

.margin-top-five {
  margin-top: 5px;
}

.pad-right-ten {
  padding-right: 10px;
}

.text-left {
  text-align: left;
}

.text-bold {
  font-weight: bold;
}

.text-white {
  color: #fff;
}
.text-right {
  text-align: right;
}
.text-left {
  text-align: left;
}
</style>
