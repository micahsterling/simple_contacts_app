<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="contact in contacts" v-bind:key="contact.id">
      {{contact.first_name}}
      {{contact.last_name}}
    </div>
  </div>
</template>
<style>
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "These are my Peeps",
      contacts: [],
    };
  },
  created: function () {
    console.log("in created");
    this.contactsIndex();
  },
  methods: {
    contactsIndex: function () {
      console.log("in contacts index");
      axios.get("http://localhost:3000/api/contacts").then((response) => {
        console.log(response.data);
        this.contacts = response.data;
      });
    },
  },
};
</script>