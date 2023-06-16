<template>
  <input type="text" name="address" id="address" v-model="query" @input="searchAddress">
</template>

<script >
let url = "https://suggestions.dadata.ru/suggestions/api/4_1/rs/suggest/address";
let token = "9e5a156fa96d01715ed43402e8801408fb4644eb";
let query = " ";
let options = {
  method: "POST",
  mode: "cors",
  headers: {
    "Content-Type": "application/json",
    "Accept": "application/json",
    "Authorization": "Token " + token
  },
  body: JSON.stringify({query: query})
};
export default {
  name:'searchAddress',
  data() {
    return {
      query: ''
    }
  },
   methods:{
     async searchAddress() {
       await fetch(url, options)
           .then(response => response.text())
           .then(result => this.query)
           .catch(error => console.log("error", error));
    }
  }
}

</script>
