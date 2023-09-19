<template>
    <div :class="{ blueColor: goVisible || blueVisible , greenColor: greenVisible}">
        <button v-if="goVisible" class="goButton" @click="go()">Go</button>
        <button v-if="stopVisible" class="stopButton" @click="stop()">Stop</button>
        <ResultDisplay :message="Resultmessage" :highscore="minTime" />
    </div>
</template>
<script>

import ResultDisplay from './Result.vue'

export default {
    name: 'GoButton',
    data() {
        return {
            goVisible: true,
            stopVisible: false,
            blueVisible: true,
            greenVisible: false,
            intervalId: null,
            interval: null,
            Resultmessage: 'Click go to your reaction time',
            startTime: null,
            formattedTime: '',
            minTime: 'N/A'
        }
    },
    methods: {
        go() {
            this.goVisible = false
            this.stopVisible = true
            this.intervalId = setTimeout(() => {
                this.blueVisible = false;
            }, 3000);
            this.interval = setTimeout(() => {
                this.greenVisible = true;
                this.startTime = Date.now();
            }, 3000);
            this.Resultmessage = "Pay attention. Click stop when the color changes"
        },

        stop() {
            this.goVisible = true
            this.stopVisible = false
            this.blueVisible = true
            clearInterval(this.interval);
            clearInterval(this.intervalId);
            if (this.greenVisible) {
                const endTime = Date.now();
                const reactionTime = (endTime - this.startTime) / 1000;
                this.formattedTime = reactionTime.toFixed(2) + ' sec';
            } else {
                this.formattedTime = 'N/A';
            }
            this.greenVisible ? this.Resultmessage = `Your time was: ${this.formattedTime}. Try again! ` : this.Resultmessage = "Too quick... Try again!"
            if (this.formattedTime &&  (this.minTime > this.formattedTime)) {
                    this.Resultmessage = `You've set a new high score: ${this.formattedTime}`
                    this.minTime = this.formattedTime
            }
            this.greenVisible = false
            clearInterval(this.startTime);
            clearInterval(this.formattedTime);
        }
    },
    components: {
        ResultDisplay
    }
}

</script>

<style scoped>
.greenColor {
    width: 100%;
    height: 100vh;
    background-color: rgb(32, 146, 40);
}

.blueColor {
    width: 100%;
    height: 100vh;
    background-color: rgb(32, 34, 146);
}

.err {
    width: 100%;
    height: 100vh;
    background-color: green;
}

.goButton {
    padding: 3rem 15rem;
    background-color: rgb(4, 171, 4);
    font-size: 40px;
    margin-top: 10%;
    margin-left: 30%;
    color: white;
    border: none;
    border-radius: 1rem;
    cursor: pointer;
}

.stopButton {
    padding: 3rem 15rem;
    background-color: rgb(171, 58, 35);
    font-size: 40px;
    margin-top: 10%;
    margin-left: 30%;
    color: white;
    border: none;
    border-radius: 1rem;
    cursor: pointer;
}
</style>