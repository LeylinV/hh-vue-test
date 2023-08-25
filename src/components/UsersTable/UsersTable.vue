<template>
  <div class="table">
    <TableHead @selectedSort="handleSelectedSort"/>
    <div>
      <template v-for="user in users">
        <TableRow :user="user" :key="user.id" />
      </template>
    </div>
  </div>
</template>

<script>
import TableRow from "./TableRow/TableRow.vue";
import TableHead from "./TableHead/TableHead.vue";

export default {
  components: {TableHead, TableRow},
  props:{
    users: Array,
  },
  data() {
    return {

    }
  },
  methods:{
    handleSelectedSort(sort) {
      this.$emit('selectedSort', sort);
    }
  }
};
</script>

<style scoped>
.table {
  width: 100%;
}
</style>
