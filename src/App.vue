<template>
    <div id="app">
        <Timer :timer="timer" :saveTime="saveTime"/>
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
            savedTime: undefined,
            id: 0
        };
    },

    computed: {
        timer: function() {
            if(this.savedTime) {
                let tmp = this.savedTime;
                this.savedTime = undefined;
                return tmp;
            }
            return this.lights[this.id].time;
        }
    },

    methods: {

        changeColor( color, time ){

            if(typeof color == "string") {
                let matched = false;
                for(let i = 0; i < this.lights.length; i++){
                    if(color != this.lights[i].color) continue;
                    this.id = i;
                    matched = true;
                    break;
                }
                if(!matched) this.id = 0;
            }
            else if( +color >= 0 &&
                +color < this.lights.length ) {
                this.id = color
            } 
            else if( this.id < this.lights.length - 1 ) {
                this.id++;
            }
            else {
                this.id = 0;
            }

            if( !( time && +time > 0 && +time <= this.lights[this.id].time ) ) {
                time = this.lights[this.id].time;
            }
            this.savedTime = time;

            this.$router.push(this.lights[this.id].color);
            setTimeout(() => {
                this.changeColor();
            }, time * 1000);
        },

        saveTime(timeLeft) {
            localStorage.timer = timeLeft;
            localStorage.id = this.id;
        }

    },

    mounted: function() {
        let timer   = +localStorage.timer;
        let id      = localStorage.id >= 0 ? +localStorage.id : this.$route.params.color;
        this.changeColor( id  || 0, timer );
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