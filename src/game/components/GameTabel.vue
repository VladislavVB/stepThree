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
        if (
          this.check[0].text === this.check[1].text &&
          this.check[0] != this.check[1]
        ) {
          this.check.forEach((elem) => {
            elem.okey = true;
          });
        }
        setTimeout(() => {
          this.check.forEach((item) => {
            item.hide = false;
          });
          this.check = [];
        }, 300);
      }

      const flatData = JSON.parse(JSON.stringify(this.data)).flat();
      if (flatData.filter((el) => el.okey).length === flatData.length) {
        this.$emit("onGamePasset", true);
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
    }
  },
};
</script>

<style lang="scss" scoped>
.game {
  border: 5px solid #fff;
  padding: 10px;
  display: grid;
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
