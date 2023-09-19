<template>
    <div class="resultDiv">
        <h4>{{ message }}</h4>
        <br />
        <h2>
            Your High Score : {{ highscore }}
        </h2>
    </div>
</template>

<script>
export default {
    name: 'ResultDisplay',
    props: ['message', 'highscore']
}
</script>
<style scoped>
* {
    margin: 0;
    padding: 0;
    font-family: sans-serif;
  }
.resultDiv {
    padding: 2rem 0 2rem 2rem;
    width: 35rem;
    background-color: white;
    margin-top: 3rem;
    font-size: 20px;
    margin-left: 32%;
    border-radius: 1rem;
  
}
</style>