<template>
  <div v-for="row in rows" :key="row">
    <div v-for="col in columns" :key="col"></div>
  </div>
</template>

<script>
export default {
  name: "GameTabel",
  props: {
    rows: Number,
    columns: Number,
  },
};
</script>

<style lang="scss" scoped></style>
