<template>
    <p>{{ timeLeft }}</p>
</template>

<script>
export default {

    props:[ "timer" ],

    data(){
        return {
            timeStart: new Date,
            timeLeft: this.timer
        };
    },

    watch: {
        timer: function(){
            this.timeStart = new Date;
        }
    },

    methods: {
        tickTime(){
            const currTime = new Date;
            const timePassed = currTime - this.timeStart;
            this.timeLeft = (this.timer - timePassed / 1000).toFixed(1);
        }
    },

    created: function(){
        setInterval(() => {
            this.tickTime();
        }, 100);
    },

    updated: function() {
        this.tickTime();
    }
}
</script>

<style>
p {
    width: inherit;
    text-align: center;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-size: 2rem;
}
</style>