<template>
    <div id="app">
        <p id="timer">10s</p>
        <div id="main">
          <div id="green"></div>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return {
            color: "green"
        };
    }
}
</script>

<style>
#main{
    background-color: grey;
    height: 400px;
    width: 400px;
    border-radius: 50%;
}
</style>