<template>
    <div id="app">
        <Timer :time="lights[id].time"/>
        <div id="main">
          <Light :color="lights[id].color"/>
        </div>
    </div>
</template>

<script>
import Light from "./components/Light.vue";
import Timer from "./components/Timer.vue";

const green  = { color: "green",  time: 15 };
const red    = { color: "red",    time: 10 };
const yellow = { color: "yellow", time:  3 };

const lights = [
    green,
    yellow,
    red,
    yellow
];

export default {
    data() {
        return  {
            lights,
            id: 0
        };
    },
    methods: {
        changeColor(){
            if(this.id < lights.length - 1) {
                this.id++;
            } else {
                this.id = 0;
            }
            setTimeout(() => {
                this.changeColor();
            }, this.lights[this.id].time * 1000);
        }
    },
    mounted: function() {
        this.changeColor();
    },
    components: {
        Light, Timer
    }
};
</script>

<style>
#app > div {
    margin: 0 auto;
    width: 400px;
}
#main{
    background-color: grey;
    height: 400px;
    border-radius: 50%;
}
</style>