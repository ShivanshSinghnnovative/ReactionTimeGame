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
.resultDiv {
    padding: 2rem 7rem;
    width: fit-content;
    background-color: white;
    margin-top: 3rem;
    font-size: 20px;
    margin-left: 30%;
    border-radius: 1rem;
}
</style>