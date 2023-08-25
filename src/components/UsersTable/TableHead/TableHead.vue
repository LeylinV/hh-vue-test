<template>
  <div class="table-head">
    <div @click="handleSelectedSort('name')">Имя</div>
    <div @click="handleSelectedSort('tel')">Телефон</div>
  </div>
</template>

<script>
export default {
  methods:{
    handleSelectedSort(sort) {
      this.$emit('selectedSort', sort);
    }
  }
}
</script>

<style scoped>
.table-head{
  display: flex;
  justify-content: flex-end;
}
.table-head > div {
  width: 50%;
  padding: 12px 18px;
  font-size: 18px;
  font-weight: 700;
  border: 2px solid #3d3d3d;
  margin: 0 -2px 0 0;
  cursor: pointer;
}
.table-head > div:last-of-type {
  border-left: none;
}
</style>
