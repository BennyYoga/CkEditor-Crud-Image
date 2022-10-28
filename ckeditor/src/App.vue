<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App" /> -->
  <ListArticle v-bind:editorData='editorData' @get-data-ID="getID"/>
  <FormArticle @add-data-article="addDataArticle" v-bind:propsDataEditor='editorData' v-bind:getId='getId'/>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import FormArticle from './components/formArticle.vue';
import axios from 'axios'
import ListArticle from './components/listArticle.vue';

export default {
  name: 'App',
  components: {
    ListArticle,
    FormArticle
  },
  data() {
    return {
      editorData: "",
      getId : ""
    }
  },
  mounted() {
    try {
      axios.get("http://localhost:3000/data")
        .then((response) => {
          this.editorData = response.data
        })
    }
    catch (error) {
      console.log(error.message);
    }
  },
  methods: {
    addDataArticle(dataEditor) {
      try {
        axios.post("http://localhost:3000/data", dataEditor)
          .then(response => {
            this.editorData = [...this.dataEditor, response.data]
          })
          .catch(error => {
            if (error.response) {
              alert(error.response.data.message)
            }
          })
      }
      catch (error) {
        console.log("Data Error");
      }
    },
    editorDataArticle(id, dataeditor){
      try{
        console.log(id);
        console.log(dataeditor);
      }
      catch(error){
        console.log(error);
      }
    },
    getID(data){
      this.getId = data;
      alert(this.getId)
    }
  }
}
</script>

<style>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
</style>
