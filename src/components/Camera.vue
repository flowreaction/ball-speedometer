<template>
    <div class="camera">
        <video autoplay class="feed"></video>
    </div>
</template>

<script>
// import * as tf from '@tensorflow/tfjs'

export default {
    name: "camera",
    data: function() {
        return {
            cameraConstraints: {
                video: {
                    frameRate: { 
                        min: 20,
                        ideal: 30,
                        max: 60
                        },
                    facingMode: "environment",
                    width: { ideal: 1920 },
                    height: { ideal: 1200 }
                }
            }
        }
    },
    methods: {
        init () {
            if ('mediaDevices' in navigator && 'getUserMedia' in navigator.mediaDevices){
                navigator.mediaDevices.getUserMedia(this.cameraConstraints)
                    .then(stream => {
                        const videoPlayer = document.querySelector("video");
                        videoPlayer.srcObject = stream;
                        videoPlayer.play();
                    })
            }
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

<style>
    .camera {
        position: absolute;
        top: -50%;
        left: -50%;
        width: 200%;
        height: 200%;
    }
    .feed {
        position: absolute;
        top: 0;
        bottom: 0;
        right: 0;
        left: 0;
        margin: auto;
        min-width: 50%;
        min-height: 50%;
    }

</style>