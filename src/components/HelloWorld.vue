<template>
  <div class="wrapper">
    <div
      @click="checkCard(item)"
      v-for="item in cards"
      :key="item"
      class="card"
    >
      {{ item.text }}
      <div v-bind:class="{ active: item.hide, okey: item.okey } " class="hide"></div>
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
        { text: "1", hide: false, okey: false },
        { text: "2", hide: false, okey: false },
        { text: "1", hide: false, okey: false },
        { text: "4", hide: false, okey: false },
        { text: "3", hide: false, okey: false },
        { text: "4", hide: false, okey: false },
        { text: "2", hide: false, okey: false },
        { text: "3", hide: false, okey: false },
      ],
      check: [],
    };
  },
  methods: {
    checkCard(item) {
      this.check.push(item);
      item.hide = true;
      // console.log(this.check);
      // console.log(item);
    },
  },
  updated() {
    console.log(this.check);

    if (this.check.length > 2) {
      this.check.forEach((item) => {
        item.hide = false;
      });
      this.check = [];
      console.log('dss');
    }

    if (this.check.length >= 2) {
      if (this.check[0].text === this.check[1].text) {

      
        this.check.forEach(elem => {
          elem.okey = true;
          console.log('ok');
        })
      
      }
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
</style>
