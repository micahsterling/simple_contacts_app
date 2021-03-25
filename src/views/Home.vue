<template>
  <div class="home">
    <h1>{{ message }}</h1>
      <h3>Make a New Contact</h3>
      <p>
        First Name: 
        <input type="text" v-model="newContactFirstName">
      </p>
      <p>
        Last Name:   
        <input type="text" v-model="newContactLastName">
      </p>
      <p>
        Email: 
        <input type="text" v-model="newContactEmail">
      </p>
      <p>
        Phone Number: 
        <input type="text" v-model="newContactPhoneNumber">
      </p>
      <button v-on:click="contactsCreate">Add new Peep</button>
    <div v-for="contact in contacts" v-bind:key="contact.id">
      {{contact.first_name}}
      {{contact.last_name}}
      <img v-bind:src="contact.image"> 
    </div>
  </div>
</template>
<style>
img {
  width: 100px;
}
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "These are my Peeps",
      newContactFirstName: "",
      newContactLastName: "",
      newContactEmail: "",
      newContactPhoneNumber: "",
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
    contactsCreate: function () {
      console.log("in contacts create");
      console.log(this.newContactFirstName);

      var params = {
        first_name: this.newContactFirstName,
        last_name: this.newContactLastName,
        email: this.newContactEmail,
        phone_number: this.newContactPhoneNumber,
      };
      axios
        .post("http://localhost:3000/api/contacts", params)
        .then((response) => {
          console.log(response.data);
          this.contacts.push(response.data);
          this.newContactFirstName = "";
          this.newContactLastName = "";
          this.newContactEmail = "";
          this.newContactPhoneNumber = "";
        });
    },
  },
};
</script>