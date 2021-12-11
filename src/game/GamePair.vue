<template>
  <form @submit.prevent class="game__form">
    <p v-bind:class="{ active: errorValidate }" class="error">
      Данные не корректны
    </p>
    <input v-model="gameColumn" placeholder="колонки" type="number" />
    <input v-model="gameRow" placeholder="строки" type="number" />
    <button @click="printGame()">Запустить</button>
  </form>

  <GameTimer />

  <div class="game">
    <GameTabel @onGamePasset="onGamePasset()" :rows="gameRow" :columns="gameColumn" :cards="cards" />
  </div>

  <button v-bind:class="{ hide: btnReapetGame }" class="game__repeat">
    Сыграть еще раз
  </button>
</template>

<script>
import GameTabel from "./components/GameTabel.vue";
import GameTimer from "./components/GameTimer.vue";

export default {
  name: "GamePair",
  components: {
    GameTabel,
    GameTimer,
  },

  data() {
    return {
      // errors: [],
      errorValidate: false,
      gameColumn: null,
      gameRow: null,
      btnReapetGame: true,
      // isHide: false,
      cards: [
        // { text: "1", hide: false, okey: false },
        // { text: "2", hide: false, okey: false },
        // { text: "1", hide: false, okey: false },
        // { text: "4", hide: false, okey: false },
        // { text: "3", hide: false, okey: false },
        // { text: "4", hide: false, okey: false },
        // { text: "2", hide: false, okey: false },
        // { text: "3", hide: false, okey: false },
        // { text: "5", hide: false, okey: false },
        // { text: "5", hide: false, okey: false },
        // { text: "6", hide: false, okey: false },
        // { text: "7", hide: false, okey: false },
        // { text: "6", hide: false, okey: false },
        // { text: "7", hide: false, okey: false },
        // { text: "8", hide: false, okey: false },
        // { text: "8", hide: false, okey: false },
      ],
      check: [],
    };
  },

  methods: {
    onGamePasset() {
      this.btnReapetGame = false
    },
    validateForm(column, row) {
      return !(
        column < 2 ||
        column > 10 ||
        row < 2 ||
        row > 10 ||
        (column * row) % 2 !== 0
      );
    },
    printGame() {
      if (!this.validateForm(this.gameColumn, this.gameRow)) {
        this.errorValidate = true;
        console.log("111111111111111111111111");
        return;
      }
      this.errorValidate = false;
      // console.log(validateForm);
      // console.log(this.gameColumn);
      // console.log(this.gameRow);
      let resData = [];
      for (let i = 0; i < this.gameColumn * this.gameRow; i += 2) {
        const data = {
          text: i,
          hide: false,
          okey: false,
        };
        resData[i] = { ...data };
       resData[i + 1] = { ...data };
      }
      resData.sort(() => Math.random() - 0.5);

      this.cards = resData
      
      console.log(resData);
      // this.gameColumn = "";
      // this.gameRow = "";
      //ну тут непонятно как ьез
      // const
    },
  },
  updated() {
    // let a = false;
    // this.cards.forEach((elem) => {
    //   if (!elem.okey) {
    //     a = true;
    //   }
    // });
    // if (!a) {
    //   this.btnReapetGame = false;
    // }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
.error {
  display: none;
  &.active {
    display: block;
  }
}
.game {
  border: 5px solid #fff;
  padding: 10px;
  // display: grid;
  // grid-template-columns: 1fr 1fr 1fr;
  // grid-template-rows: 1fr 1fr 1fr;
  // gap: 10px 10px;
  // max-width: 280px;
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
