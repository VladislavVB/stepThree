<template>
  <div class="wrapper">
    <div @click="cheackCard(item)" v-for="item in cards" :key="item" class="card">
      {{item.text}}
      <div v-bind:class="{active: item.hide}" class="hide"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      // isHide: false,
      cards: [
        { name: "card1", text: "1", hide: false },
        { name: "card2", text: "2", hide: false },
        { name: "card3", text: "1", hide: false },
        { name: "card4", text: "4", hide: false },
        { name: "card5", text: "3", hide: false },
        { name: "card6", text: "4", hide: false },
        { name: "card7", text: "2", hide: false },
        { name: "card8", text: "3", hide: false },
      ],
      cheack: []
    };
  },
  methods: {
    cheackCard(item) {
      this.cheack.push(item)
      item.hide = true;
      console.log(this.cheack);
      console.log(item);
    }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.wrapper {
  border: 5px solid #fff;
  padding: 10px;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  max-width: 280px;
}
.card {
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
    }
  }
}
</style>
