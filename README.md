![alt text](https://github.com/imrancse94/vue-table-pagination/blob/main/screenshot.png?raw=true)


:earth_africa: Installation
---------------------------

  npm install --save vue-laravel-table-pagination

:wave: Usage
------------

At the root of your project, just before creating your Vue application, import the `vue-laravel-table-pagination` plug-in, and add it to the Vue global with the following code:

#### Example - `main.js`

``` js
import Vue from 'vue'
import Pagination from 'vue-laravel-table-pagination'

Vue.component('Pagination', Pagination)

### `App.vue`

<template>
  <div>
    <Pagination
        :data="data"
        @paginateTo="getPaginateData"
      />
  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
        return {
            data: {
            "current_page": 1,
            "data": [
                {
                    "id": 3,
                    "name": "Company List",
                },
                {
                    "id": 10,
                    "name": "Module List"
                    
                }
            ],
            "first_page_url": "<your api>?page=1",
            "from": 1,
            "last_page": 5,
            "last_page_url": "<your api>?page=5",
            "next_page_url": "<your api>?page=2",
            "path": "<your api>",
            "per_page": 2,
            "prev_page_url": null,
            "to": 2,
            "total": 10
        }
        }
      },
     methods:{
       getPaginateData(){
        var current_page = this.$router.currentRoute.query;
        apiMethod(current_page).then((response_data) => {
          this.data = response_data;
        });
       }
     } 
}
</script>
```
