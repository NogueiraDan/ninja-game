<template>
  <div class="block" v-if="showBlock" v-on:click="stopTimer()">Click me</div>
</template>

<script>
import { onMounted, onUnmounted, onUpdated, ref} from "vue";

export default {
  props: ["delay"],
  setup(props, ctx) {
    const showBlock = ref(false);
    const timer = ref(null);
    const reactionTime = ref(0)


    const startTimer = ()=>{
      timer.value = setInterval(()=>{
        reactionTime.value +=10;
      }, 10)

    }

    const stopTimer = ()=>{
      clearInterval(timer.value)
      ctx.emit('end', reactionTime)

    }

    onMounted(() => {
      setTimeout(()=>{
        showBlock.value = true
        startTimer()
      }, props.delay)
    });


    return {
      showBlock,
      onMounted,
      onUpdated,
      startTimer,
      stopTimer,
      timer,
      reactionTime,
    };
  },
};
</script>

<style scoped>
.block {
  width: 400px;
  border-radius: 20px;
  background: #12c396;
  color: #fff;
  text-align: center;
  padding: 100px 0;
  margin: 30px auto;
  cursor: pointer;
}
</style>
