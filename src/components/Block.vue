<template>
  <div class="block" v-if="showBlock" @click="stopTimer">click me</div>
</template>


<script>
export default {
    props: ['delay'],
    data(){
        return {
            showBlock: false,
            timer: null,
            reactionTime: 0
        }
    },
    mounted(){
        // console.log('component mounted')
        setTimeout(() => {
            this.showBlock = true;
            // console.log(this.delay)
            // when green block appears, it starts the timer
            this.startTimer();
        }, this.delay)
    },
    methods: {
        startTimer(){
            // this function will run every 10 ms(it will keep on increasing until we stop)
            this.timer = setInterval(() => {
                this.reactionTime += 10;
            }, 10)
        },
        stopTimer(){
            clearInterval(this.timer);
            // console.log(this.reactionTime);
            // to pass data from child to parent we use custom event
            this.$emit('end', this.reactionTime);
        }
    }
    // updated(){
    //     console.log('component updated')
    // },
    // unmounted(){
    //     console.log('component unmounted')
    // }
}
</script>


<style>
.block{
    width: 400px;
    border-radius: 20px;
    background: #0faf87;
    color: white;
    text-align: center;
    padding: 100px 0;
    margin: 40px auto;
}

</style>