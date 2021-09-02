<template>
  <div class="camera">
    <video autoplay playsinline class="feed"></video>
    <button id="infoBtn" @click="printInfo()">Print Info</button>
    <button id="switchCam" @click="switchCamera()">Switch Camera</button>
  </div>
</template>

<script>
// import * as tf from '@tensorflow/tfjs'
// import * as mobilenet from '@tensorflow-models/mobilenet'

export default {
  name: "camera",
  data: function() {
    return {
      currentPrediciton: {},
      stream: null,
      mediaTrack: null,
      faceUser: false,
      cameraConstraints: {
        video: {
          frameRate: {
            min: 30,
            ideal: 120,
          },
          facingMode: this.faceUser ? 'user': 'environment',
          width: { ideal: 1920 },
          height: { ideal: 1200 },
        },
      },
    };
  },
  methods: {
    async init() {
      if (
        "mediaDevices" in navigator &&
        "getUserMedia" in navigator.mediaDevices
      ) {
        console.log("Getting camera from user");
        this.stream = await navigator.mediaDevices.getUserMedia(
          this.cameraConstraints
        );
        this.mediaTrack = await this.stream.getVideoTracks()[0];
        const videoPlayer = document.querySelector("video");
        videoPlayer.srcObject = this.stream;
        videoPlayer.play();
      }
    },
    printInfo() {
      console.log(this.mediaTrack.getSettings());
    },
    switchCamera(){
      console.log("switching camera")
      this.faceUser = !this.faceUser;
      this.mediaTrack.applyConstraints(this.cameraConstraints)
      console.log(`faceUser: ${this.faceUser}`)
    }
  },
  beforeMount() {
    this.init();
  },
  created() {
    // const cocoSSD = require('@tensorflow-models/coco-ssd');
    // (async ())
  },
};
</script>

<style scoped>
.camera {
  position: absolute;
  top: 0;
  left: 0;

}
.feed {
  top: 0;
  left: 0;
  width: 100vw;
  max-height: 100vh;
  z-index: 0;
}
button {
  position: absolute;
  top: 90%;
  transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  background-color: #555;
  color: white;
  font-size: 16px;
  padding: 12px 24px;
  border: none;
  cursor: pointer;
  border-radius: 5px;
}

#infoBtn {

  left: 40%;
}
#switchCam {
  left: 60%;
}
</style>
