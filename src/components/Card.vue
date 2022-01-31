<template>
  <div class="m-4 mt-5 card-container shadow rounded bg-black mx-auto">
    <div class="card-row"
      v-for="(n, rowIndex) in rowsCols"
      :key="rowIndex"
    >
      <div class="d-inline-block card-text text-black bg-white ff-serif text-center"
        v-for="(n, colIndex) in rowsCols"
        :key="colIndex"
      >
          {{
            String.fromCharCode(
              arrayOfAlphabetASCII[rowIndex * rowsCols + colIndex]
            )
          }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: {
    rowsCols: Number,
  },
  data() {
    return {
      arrayOfAlphabetASCII: this.shuffleArray(
        Array.from({ length: 26 }, (x, i) => i + 65)
      ),
    };
  },
  methods: {
    shuffleArray(array) {
      for (let i = array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
      }
      return array;
    },
  },
};
</script>

<style scoped lang="scss">
.card-container {
  border: solid black;
  border-width: 12px;
  border-radius: 4px;
  background-color: black;
  margin-top: 34px !important;
}

.card-row {
  margin-bottom: 12px;

  &:last-child {
    margin-bottom: 0;
  }
}

.card-text {
  width: 60px;
  height: 60px;
  font-family: "Roboto Slab", serif;
  font-weight: 900;
  font-size: 36px;
  line-height: 60px;
  margin: 0 6px;

  &:first-child {
    margin-left: 0;
  }

  &:last-child {
    margin-right: 0;
  }
}
</style>