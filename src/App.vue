<template>
  <div id="app" >
    <div class="wrapper mx-auto" style="max-width: 652px;">
      <div class="h1 mx-5 text-black">Card Generator</div>

      <div class="d-flex flex-column align-items-center mx-5">
        <div class="card w-100 shadow rounded">
          <div class="card-body pb-0">
            <div class="row">
              <div class="form-group d-flex flex-row flex-wrap col-sm">
                <div class="d-flex flex-row text-nowrap mb-3">
                  <label class="col-form-label">Generate</label>
                  <div class="px-2">
                    <input
                      class="form-control"
                      v-model.number="numberOfCards"
                      min="0"
                      max="5"
                      type="number"
                      placeholder="# of Cards"
                    />
                  </div>
                  <label class="col-form-label"
                    >random cards,&nbsp;
                  </label>
                </div>
                <div class="d-flex flex-wrap text-nowrap mb-3">
                  <label class="col-form-label"
                    >each with
                  </label>
                  <div class="px-2">
                    <input
                      class="form-control"
                      v-model.number="numberOfRowsColumns"
                      min="0"
                      max="5"
                      type="number"
                      placeholder="# of Rows & Columns"
                    />
                  </div>
                  <label class="col-form-label">rows/columns.</label>
                </div>
              </div>
              <div class="col-sm-auto mt-">
                <button
                  type="button"
                  class="btn btn-primary w-100 ms-auto mb-3"
                  :disabled="isDisabled"
                  v-on:click="generateCards()"
                >
                  Generate
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- Card Area -->
    <div v-if="cards.length > 0" class="d-flex flex-column">
      <Card v-for="(card,index) in cards" :key="card.id" v-bind:rowsCols="card.rowCols"></Card>
    </div>
  </div>
</template>

<script>
import Card from "./components/Card";

export default {
  name: "App",
  data() {
    return {
      showCardContainer: false,
      numberOfCards: 0,
      numberOfRowsColumns: 0,
      MAX_VAL: 5,
      cards: []
    };
  },
  components: {
    Card,
  },
  methods: {
    generateCards() {
      this.cards.splice(0);
      for (let i = 0; i < this.numberOfCards; i++) this.cards.push({rowCols: this.numberOfRowsColumns, id: Math.random()});

    },
  },
  computed: {
    isDisabled() {
      return !(
        this.numberOfCards > 0 &&
        this.numberOfCards < this.MAX_VAL + 1 &&
        this.numberOfRowsColumns > 0 &&
        this.numberOfRowsColumns < this.MAX_VAL + 1
      );
    },
  },
};
</script>

<style lang="scss">
$font-family-base: "Hind", sans-serif;
$font-family-serif: "Roboto Slab", serif;
$headings-font-family: $font-family-serif;
$btn-font-family: $font-family-serif;
$font-size-base: .875rem;
$box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
$btn-font-weight: 500;

$h1-font-size: 48px;
$spacer: 0.75rem;
$spacers: (
  0: 0,      // 0
  1: 4px,    // 4px
  2: 8px,    // 8px
  3: 12px,   // 12px
  4: 16px,   // 16px
  5: 20px,   // 20px
  6: 24px,   // 24px
  7: 28px,   // 28px
  8: 32px,   // 32px
  9: 36px,   // 36px
);


@import "~bootstrap/scss/bootstrap";
@import url("https://fonts.googleapis.com/css2?family=Roboto+Slab:wght@100;200;300;400;500;600;700;800;900&display=swap");
@import url('https://fonts.googleapis.com/css2?family=Hind&display=swap');

:root {
  background-color: rgb(221, 221, 221);
}

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 60px;
  background-color: rgb(221, 221, 221);

  input.form-control {
    width: 56px;
  }

  .h1 {
    font-weight: 700;
  }

}
</style>