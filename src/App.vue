<template>
  <v-app>
 <div class="text-center">
    <v-pagination
      v-bind:value="page"
      v-model="page"
      :length="5"
      :total-visible="7"
      v-on:input="sendRequest"
    ></v-pagination>
    {{page}}<br>
    {{responseData}}
  </div>
  </v-app>
</template>

<script>
import axios from 'axios';

export default {
  name: "App",

  data: () => ({
    //
    page: 1,
    responseData:''

  }),
  methods:{
    async sendRequest(){
      console.log(this.page);
      axios.get("http://localhost:3000/users?page="+this.page+"&limit=2")
        .then(response => this.responseData = response.data)
        .catch(error => {
      this.errorMessage = error.message;
      console.error("There was an error!", error);
    });

    },
  }
};
</script>
