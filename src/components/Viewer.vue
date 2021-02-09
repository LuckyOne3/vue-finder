<template>
  <div class="wrapper-inner d-flex w-100 flex-column">
    <div v-if=json>{{ json.data[0].name }}</div>
    <div v-else-if=childrens>
      <div v-for="item in childrens">{{ item.name }}</div>
    </div>
    <div v-else-if=preview>
      <div v-if="preview[0].store_name.indexOf('pdf') !== -1">
        <div>
          {{ currentPage }} / {{ pageCount }}
          <div v-on:click="previousPdfPage">previous</div>
          <div v-on:click="nextPdfPage">next</div>
          <pdf
              :src=preview[0].store_name
              @num-pages="pageCount = $event"
              @page-loaded="currentPage = $event"
              :page="currentPage"
          ></pdf>

        </div>

      </div>
      <div v-else>
        <xlsx-read :file=require('./../assets/uYidnvrEkJ5tsjlCGpXU7qcjCdNiUX.xlsx') >
          <xlsx-table />
        </xlsx-read>
      </div>
    </div>
    <div v-else></div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
// @ts-ignore
import pdf from 'vue-pdf'
// @ts-ignore
import {XlsxRead,XlsxTable} from "vue-xlsx/dist/vue-xlsx.es.js"




export default Vue.extend({
  name: 'Viewer',
  props: {
    json: {} as any,
    childrens: {} as any,
    preview: {} as any,
  },
  data() {
    return {
      currentPage: 1,
      pageCount: 0,
      file:null
    }
  },
  components: {
    pdf,
    XlsxRead,
    XlsxTable
  },
  methods: {
    nextPdfPage: function () {
      if(this.$data.pageCount > this.$data.currentPage)
      this.$data.currentPage = this.$data.currentPage + 1
    },
    previousPdfPage: function () {
      if (this.$data.currentPage !== 1)
        this.$data.currentPage = this.$data.currentPage - 1
    },

  }
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.wrapper-inner div {
  text-align: center;
}

h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
