<template>
  <div class="vue-table-pagination">
    <ul class="pagination m-0">
      <li class="page-item">
        <button
          type="button"
          :disabled="!data.prev_page_url"
          @click.prevent="paginateTo(data.current_page - 1)"
          class="page-link"
        >
          «
        </button>
      </li>
      <li
        v-for="index in data.last_page"
        :key="index"
        :class="index === data.current_page ? 'active' : ''"
        class="page-item"
      >
        <button
          type="button"
          v-if="data.last_page > 1"
          @click.prevent="paginateTo(index)"
          class="page-link"
        >
          {{ index }}
        </button>
      </li>
      <li class="page-item">
        <button
          type="button"
          :disabled="!data.next_page_url"
          @click.prevent="paginateTo(data.current_page + 1)"
          class="page-link"
        >
          »
        </button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "VueTablePagination", // vue component name
  props: {
    data: {
      type: Array,
      default() {
        return [];
      },
    },
  },

  methods: {
    paginateTo(page) {
      if (this.$router.currentRoute.query.page != page) {
        this.paginateFunction(page);
      }
    },

    paginateFunction(page) {
      var queryparams = Object.assign({}, this.$router.currentRoute.query, {
        page: page,
      });

      this.$router
        .replace({
          path: this.$router.currentRoute.path,
          query: queryparams,
        })
        .catch(() => {});

      this.$emit("paginateTo", page);
    },
  },
};
</script>

<style scoped>
.vue-table-pagination .pagination {
  display: flex;
  padding-left: 0;
  list-style: none;
  border-radius: 4px;
}
.vue-table-pagination .m-0 {
  margin: 0 !important;
}

.vue-table-pagination .page-item.active .page-link {
  z-index: 3;
  color: #fff;
  background-color: #007bff;
  border-color: #007bff;
}

.vue-table-pagination .page-link {
  position: relative;
  display: block;
  padding: 8px 12px;
  margin-left: -1px;
  line-height: 1.25;
  color: #007bff;
  background-color: #fff;
  border: 1px solid #dee2e6;
}

.vue-table-pagination .page-item:last-child .page-link {
  border-top-right-radius: 4px;
  border-bottom-right-radius: 4px;
}

.vue-table-pagination .page-link:hover {
  z-index: 2;
  color: #0056b3;
  text-decoration: none;
  background-color: #e9ecef;
  border-color: #dee2e6;
}

.vue-table-pagination button:not(:disabled) {
  cursor: pointer;
}

.vue-table-pagination [type=button], .vue-table-pagination button {
    -webkit-appearance: button;
}
</style>
