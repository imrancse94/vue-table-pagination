<script>
import Vue from 'vue';
import VueTablePagination from '@/vue-table-pagination.vue';

export default Vue.extend({
  name: 'ServeDev',
  components: {
    VueTablePagination
  }
});
</script>

<template>
  <div id="app">
    <vue-table-pagination />
  </div>
</template>
