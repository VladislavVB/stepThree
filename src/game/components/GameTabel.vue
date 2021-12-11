<template>
  <div class="game__cards">
    <div class="game__cards-row" v-for="row in data" :key="row">
      <div v-for="item in row" :key="item">
        <div @click="checkCard(item)" class="game__card">
          {{ item.text }}
          <div
            v-bind:class="{ active: item.hide, okey: item.okey }"
            class="hide"
          ></div>
        </div>
      </div>
    </div>
  </div>
  <!-- <div v-for="row in rows" :key="row">
    <div v-for="col in columns" :key="col"> -->
  <!-- <div
    @click="checkCard(item)"
    v-for="item in cards"
    :key="item"
    class="game__card"
  >
    {{ item.text }}
    <div
      v-bind:class="{ active: item.hide, okey: item.okey }"
      class="hide"
    ></div>
  </div> -->
  <!-- </div>

  </div> -->
</template>

<script>
export default {
  name: "GameTabel",
  props: {
    rows: Number,
    columns: Number,
    cards: Array,
  },
  data() {
    return {
      check: [],
      data: [],
    };
  },

  methods: {
    transformDataToMatrix(data, row, columns) {
      const result = [];
      let y = 0;

      for (let i = 0; i < row; i++) {
        result[i] = [];
        for (let j = 0; j < columns; j++) {
          result[i].push(data[y]);
          y++;
        }
      }

      return result;
    },
    checkCard(item) {
      this.check.push(item);
      item.hide = true;
      if (this.check.length >= 2) {
        if (this.check[0].text === this.check[1].text) {
          this.check.forEach((elem) => {
            elem.okey = true;
          });
        }
        setTimeout(() => {
          this.check.forEach((item) => {
            item.hide = false;
          });
          this.check = [];
        }, 500);
      }

      let flag = true; 
      const flatData = JSON.parse(JSON.stringify(this.data));
      flatData.flat();

      flatData.forEach((elem) => {
        console.log(elem);
        if (!elem.okey) {
          flag = false;
        }
      });
      console.log(flatData);
      if (flag) {
        console.log('222222');
        this.$emit('onGamePasset', true)
        // this.btnReapetGame = false;
      }
    },
  },
  updated() {
    if (this.cards.length) {
      this.data = this.transformDataToMatrix(
        this.cards,
        this.rows,
        this.columns
      );
      // console.log(this.cards);
    }
  },
};
</script>

<style lang="scss" scoped>
.game {
  border: 5px solid #fff;
  padding: 10px;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 1fr 1fr 1fr;
  // gap: 10px 10px;
  // max-width: 280px;
  &__cards {
    display: flex;
    flex-direction: column;
    &-row {
      display: flex;
    }
  }
  &__form {
    display: flex;
    flex-direction: column;
    margin-bottom: 50px;
    margin-top: 50px;
    input {
      border: none;
      margin-bottom: 20px;
      padding: 10px 20px;
      border-radius: 5px;
    }
    button {
      border: none;
      padding: 10px 20px;
      border-radius: 5px;
      cursor: pointer;
    }
  }
  &__repeat {
    cursor: pointer;
    margin-top: 30px;
    border-radius: 10px;
    color: #fff;
    padding: 15px 30px;
    // text-transform: uppercase;
    background-color: #336b33;
    border: 2px solid #fff;
    transition: 0.5s;
    opacity: 1;
    &.hide {
      opacity: 0;
      visibility: hidden;
    }
  }
  &__card {
    width: 50px;
    height: 50px;
    margin: 10px;
    cursor: pointer;
    background-color: #336b33;
    color: #fff;
    display: flex;
    justify-content: center;
    align-items: center;
    transition: 1.5s;
    position: relative;
    // pointer-events: none;
    .hide {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      background-color: #fff;
      height: 100%;
      transition: 0.5s;
      &.active {
        border-radius: 20px;
        width: 0;
        height: 0;
        pointer-events: none;
      }
      &.okey {
        position: absolute;
        width: 0;
        height: 100%;
        border: 1px solid #fff;
        pointer-events: none;
      }
    }
  }
}
</style>
