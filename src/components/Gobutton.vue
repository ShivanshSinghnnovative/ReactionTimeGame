<template>
    <button v-if="goVisible" class="goButton" @click="toggleVisibility('start')">Go</button>
    <button v-if="stopVisible" class="stopButton" @click="toggleVisibility('stop')">Stop</button>
</template>

<script>
export default {
    name: 'GoButton',
    data() {
        return {
            goVisible: true,
            stopVisible: false,
        }
    },
    methods: {
        toggleVisibility(action) {
            this.$emit(action);
            this.goVisible = action === 'stop';
            this.stopVisible = action === 'start';
        },
    }
}
</script>

<style scoped>
* {
    margin: 0;
    padding: 0;
    font-family: sans-serif;
  }
button {
    width: 37rem;
    padding: 2rem 0;
    font-size: 40px;
      margin-top: 10%;
    margin-left: 32%;
    margin-right: auto;
    color: white;
    border: none;
    border-radius: 1rem;
    cursor: pointer;
    text-align: center;
    align-items: center;
    justify-content: center;
   
}

.goButton {
    background-color: rgb(4, 171, 4);
}

.stopButton {
    background-color: rgb(171, 58, 35);
}
</style>