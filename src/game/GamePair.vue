<template>
  <form @submit.prevent class="game__form">
    <p v-bind:class="{ active: errorValidate }" class="error">
      Данные не корректны
    </p>
    <input v-model="gameColumn" placeholder="колонки" type="number" />
    <input v-model="gameRow" placeholder="строки" type="number" />
    <button @click="printGame()">Запустить</button>
  </form>

  <div class="timer__wrapper">
    <h1>Timer</h1>
    <div class="game__timer">{{ this.timer }}</div>
  </div>

  <div class="game">
    <div v-bind:class="{ active: playNow }" class="game__play-now">
      <!-- <img
        v-bind:class="{ active: wastedGame }"
        src="../assets/wasted.png"
        alt=""
      /> -->
    </div>
    <GameTabel
      @onGamePasset="onGamePasset()"
      :rows="gameRow"
      :columns="gameColumn"
      :cards="cards"
    />
  </div>

  <button
    @click="printGame()"
    v-bind:class="{ hide: btnReapetGame }"
    class="game__repeat"
  >
    Сыграть еще раз
  </button>
</template>

<script>
import GameTabel from "./components/GameTabel.vue";

export default {
  name: "GamePair",
  components: {
    GameTabel,
  },

  data() {
    return {
      wastedGame: false,
      NUMBER_OF_SECONDS: 10,
      timer: 10,
      timerInteval: null,
      errorValidate: false,
      gameColumn: 2,
      gameRow: 2,
      btnReapetGame: true,
      playNow: false,
      cards: [],
      check: [],
    };
  },

  methods: {
    onGamePasset() {
      this.timer = 0;
      this.btnReapetGame = false;
      this.playNow = true;
    },
    gameEnd() {
      this.wastedGame = true;
    },
    tickTack() {
      clearInterval(this.timerInteval);
      this.timerInteval = setInterval(() => {
        if (this.timer > 0 || this.timer === 1) {
          this.timer -= 1;
          this.playNow = false;
        } else {
          this.btnReapetGame = false;
          this.playNow = true;
          console.log(1);
        }
      }, 1000);
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
      this.btnReapetGame = true;
      this.playNow = false;
      this.timer = this.NUMBER_OF_SECONDS;
      if (!this.validateForm(this.gameColumn, this.gameRow)) {
        this.errorValidate = true;
        console.log("111111111111111111111111");
        return;
      }
      this.errorValidate = false;
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

      this.cards = resData;
      this.tickTack();
      console.log(resData);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
#app {
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}
.error {
  display: none;
  &.active {
    display: block;
  }
}
.timer {
  &__wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
}
.game {
  position: relative;
  width: fit-content;
  border: 5px solid #fff;
  padding: 10px;
  &__timer {
    margin-bottom: 20px;
  }
  &__play {
    &-now {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      display: flex;
      justify-content: center;
      align-items: center;
      background-color: rgba(2, 2, 2, 0.3);
      z-index: 9;
      display: none;
      &.active {
        display: flex;
      }
      img {
        display: none;
        &.active {
          display: flex;
        }
      }
      button {
        width: 200px;
        height: 50px;
        border-radius: 10px;
        background-color: #336b33;
        border: 1px solid #fff;
        color: #fff;
        z-index: 10;
        cursor: pointer;
      }
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
