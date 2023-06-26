<template>
  <div class="result">
    <h3>Tempo de reação - {{ score }}ms</h3>
    <p class="rank">{{ rank }}</p>
  </div>
</template>

<script>
import { onMounted, ref } from "vue";
export default {
  props: ["score"],
  components: {},
  setup(props) {
    const score = props.score;
    const rank = ref(null);

    onMounted(() => {
      if (score < 250) {
        rank.value = "Meu irmão! É o cosplay do Flash é? 😱😳";
        return;
      }
      if (score < 400) {
        rank.value = "Rapaz! Cê é o bichão 💪";
        return;
      }
      if (score < 500) {
        rank.value = "Foi bom, tá ligeiro. Mas dá pra melhorar 👌";
        return;
      } 
      else {
        rank.value = "Fica esperto paizão! 😜👽"
        return;
      }
    });

    return {
      score,
      rank,
    };
  },
};
</script>

<style scoped>


h3 {
  font-size: 2rem;
  color: #fff;
  font-weight: bold;
}
.rank {
  font-size: 1.5rem;
  color: #fff;
  font-weight: bold;
}
</style>
