<template>
    <div class="camera">
        <video autoplay playsinline class="feed"></video>
        <button id="infoBtn" @click="printInfo()">Print Info</button>
    </div>
</template>

<script>
// import * as tf from '@tensorflow/tfjs'
// import * as mobilenet from '@tensorflow-models/mobilenet'

export default {
    name: "camera",
    data: function() {
        return {
            currentPrediciton : {},
            stream: null,
            cameraConstraints: {
                video: {
                    // frameRate: { 
                    //     min: 30,
                    //     ideal: 1000,
                    //     // max: 240
                    //     },
                    facingMode: "environment",
                    // width: { ideal: 1920 },
                    // height: { ideal: 1200 }
                }
            }
        }
    },
    methods: {
        async init(){
            if ('mediaDevices' in navigator && 'getUserMedia' in navigator.mediaDevices){
                console.log("Getting camera from user")
                this.stream = await navigator.mediaDevices.getUserMedia(this.cameraConstraints)
                const videoPlayer = document.querySelector("video");
                videoPlayer.srcObject = this.stream;
                videoPlayer.play();
                }

        },
        printInfo (){
            console.log(this.stream.getVideoTracks()[0].getSettings())
        }
                

    },
    beforeMount(){
        this.init()
    },
    created() {
        // const cocoSSD = require('@tensorflow-models/coco-ssd');

        // (async ())
    }

}
</script>

<style scoped>

    .feed {
        position: absolute;
        top: 0;
        left: 0;
        width: 100vw;
        max-height: 100vh;
    }
    #infoBtn {
        position: absolute;
        z-index: 1;
        width: 10vw;
        height: 5vh;
        transform: translate(-50%);
    }
</style>