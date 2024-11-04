<template>
  <div class = 'container'>
    <Header/>
    <Form @key-submitted="onKeySubmit"/>
    <NewCollections :newCollections="newCollections"/>
    <Collections :collections="collections" />
    <h3>
      Hello World!
    </h3>
  </div>
</template>

<script>
import Header from './components/Header'
import Form from './components/Form'
import Collections from './components/Collections'
import NewCollections from './components/NewCollections'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    Header,
    Form,
    Collections,
    NewCollections
  },
  data(){
    return {
      collections: [],
      key: "",
      newCollections: [],
    }
  },
  methods: {
    onKeySubmit(keyValue){
      axios.get(`https://api.getpostman.com/collections?apikey=${keyValue}`)
      .then((response) => {
        this.collections = response.data.collections
        
        axios.delete("http://localhost:3000/getCollections/").then(() => {

          axios.post("http://localhost:3000/getCollections/",{key:keyValue, collections:response.data.collections}).then((response) => {
            setInterval(this.checkNewCollections,5000,keyValue)
          })
          .catch((err) => {
            console.log(err)
          });

        })
        .catch((err) => {
          console.log(err)
        });

      })
      .catch((err) => {
        console.log(err)
      });
    },
    checkNewCollections(key){
      axios.get(`https://api.getpostman.com/collections?apikey=${key}`)
      .then((response) => {
        const latestCollections = response.data.collections

        axios.get(`http://localhost:3000/getCollections/`).then((response1) => {
          const collections = response1.data.data[0].collections

          if(latestCollections.length !== collections.length){
            var newCollections = [];
            for(var i=0;i<latestCollections.length;i++){
              const uid = latestCollections[i]['uid'];
              var flag = true;
              for(var j=0;j<collections.length;j++){
                if(uid === collections[j]['uid']){
                  flag = false;
                }
              }
              if(flag){
                const addition = latestCollections[i]
                newCollections.push(addition)
              }
            }

            this.newCollections = newCollections
          }

        })
        .catch((err) => {
          console.log(err)
        });

      })
      .catch((err) => {
        console.log(err)
      });
    },
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}

</style>
