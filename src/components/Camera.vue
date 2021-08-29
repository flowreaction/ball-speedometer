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
                    frameRate: 240
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
    .feed {
        position: fixed;
        right: 0;
        top: 0;
        /* min-width: 100%;
        min-height: 100%; */
    }

</style>