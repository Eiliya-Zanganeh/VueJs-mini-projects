<template>
  <div class="result">
    <div class="title">{{ results[resultIndex].title }}</div>
    <div class="desc">
      {{ results[resultIndex].desc }}
    </div>
  </div>
</template>

<script>
export default {
  name: "ResultComponent",
  props: ["results", "totalCorrect"],
  computed: {
    resultIndex() {
      let index = 0;

      this.results.forEach((e, idx) => {
        if (e.min <= this.totalCorrect && e.max >= this.totalCorrect) {
          index = idx
        }
      });

      return index;
    }
  }
}
</script>