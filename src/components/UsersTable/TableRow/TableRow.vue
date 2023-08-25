<template>
  <div>
    <div class="row">
      <div :style="`width: ${50-level*4}%`">{{ user.name }}</div>
      <div>{{ user.tel }}</div>
    </div>
    <template v-for="subordinate in user.subordinates">
      <TableRow :user="subordinate" :key="subordinate.id" :level="level+1"/>
    </template>
  </div>
</template>


<script>
import TableRow from './TableRow.vue';

export default {
  name: 'TableRow',
  components: {
    TableRow
  },
  props: {
    user: Object,
    level: {
      type: Number,
      default: 0,
    }
  }
};
</script>

<style>
.row{
  display: flex;
  justify-content: flex-end;
}
.row > div {
  width: 50%;
  padding: 12px 18px;
  font-size: 18px;
  border: 2px solid #3d3d3d;
  margin: -2px -2px 0 0;
}
.row > div:last-of-type {
  border-left: none;
}
</style>
