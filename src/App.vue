<template>
  <div id="app">
    <div class="wrapper d-flex row">
      <div class="folders col-2 border-right">
        <Viewer v-for="(folders,index) in dataJson" :key="folders.data[0].id + '' + index" :json=folders
                    v-on:click.native="selectFolder(index)"/>
      </div>
      <div class="files col-2 border-right">
        <Viewer v-for="files in currentFilesViewer" :childrens=files.under_folder />
        <Viewer v-for="files in currentFilesViewer" :childrens=files.files
                    v-on:click.native="selectFile(files.files)"/>
      </div>
      <div class="preview col-8">
        <Viewer :preview=previewerView />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import Viewer from './components/Viewer.vue';

export default Vue.extend({
  name: 'App',
  components: {
    Viewer
  },
  data: function () {
    return {
      json: [{
        "data": [{
          "id": 5,
          "parent_id": null,
          "technical_acceptance_id": 11,
          "name": "excel",
          "created_at": "2021-02-02 17:49:05",
          "updated_at": "2021-02-02 17:49:05",
          "under_folder": [{
            "id": 6,
            "parent_id": 5,
            "technical_acceptance_id": 11,
            "name": "excel",
            "created_at": "2021-02-02 17:49:05",
            "updated_at": "2021-02-02 17:49:05",
            "files": [{
              "id": 1,
              "folder_id": 6,
              "tag_id": null,
              "name": "\u0418\u043c\u043f\u043e\u0440\u0442_ 15.01\u00a0\u044f 3.xlsx",
              "store_name": "uYidnvrEkJ5tsjlCGpXU7qcjCdNiUX.xlsx",
              "created_at": "2021-02-02 17:49:05",
              "updated_at": "2021-02-02 17:49:05"
            }]
          }],
          "files": [{
            "id": 1,
            "folder_id": 6,
            "tag_id": null,
            "name": "\u0418\u043c\u043f\u043e\u0440\u0442_ 15.01\u00a0\u044f 3.xlsx",
            "store_name": "https://example-files.online-convert.com/spreadsheet/xlsx/example.xlsx",
            "created_at": "2021-02-02 17:49:05",
            "updated_at": "2021-02-02 17:49:05"
          }]
        }], "status_code": 200
      }, {
        "data": [{
          "id": 8,
          "parent_id": null,
          "technical_acceptance_id": 11,
          "name": "pdf",
          "created_at": "2021-02-02 17:49:05",
          "updated_at": "2021-02-02 17:49:05",
          "under_folder": [{
            "id": 14,
            "parent_id": 8,
            "technical_acceptance_id": 11,
            "name": "pdf",
            "created_at": "2021-02-02 17:49:05",
            "updated_at": "2021-02-02 17:49:05",
            "files": [{
              "id": 1,
              "folder_id": 14,
              "tag_id": null,
              "name": "\u0418\u043c\u043f\u043e\u0440\u0442_ 15.01\u00a0\u044f 3.xlsx",
              "store_name": "uYidnvrEkJ5tsjlCGpXU7qcjCdNiUX.xlsx",
              "created_at": "2021-02-02 17:49:05",
              "updated_at": "2021-02-02 17:49:05"
            }]
          }],
          "files": [{
            "id": 2,
            "folder_id": 8,
            "tag_id": null,
            "name": "\u0418\u043c\u043f\u043e\u0440\u0442_ 15.01\u00a0\u044f 3.pdf",
            "store_name": "https://cdn.rawgit.com/mozilla/pdf.js/c6e8ca86/test/pdfs/calrgb.pdf",
            "created_at": "2021-02-02 17:49:05",
            "updated_at": "2021-02-02 17:49:05"
          }]
        }], "status_code": 200
      }],
      currentFiles: null,
      preview: null
    }
  },
  computed: {
    dataJson() {
      return this.$data.json
    },
    currentFilesViewer() {
      return this.$data.currentFiles
    },
    previewerView() {
      return this.$data.preview
    },
  },
  methods: {
    selectFolder: function (index: number) {
      this.$data.preview = null
      this.$data.currentFiles = this.$data.json[index].data
    },
    selectFile: function (data: any) {
      this.$data.preview =  data
    }
  },
});
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: ghostwhite;
}

.wrapper {
  min-width: 100vw;
  min-height: 100vh;
  width: 100%;
  height: 100%;
  margin: 0px !important;
}
</style>
