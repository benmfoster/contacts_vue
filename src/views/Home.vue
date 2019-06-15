<template>
  <div class="home">
    <h3>New Contact</h3>
    <div>
      <h5>First Name: <input type="text" v-model="newContactFirstName"></h5>
      <h5>Last Name: <input type="text" v-model="newContactLastName"></h5>
      <h5>Phone Number: <input type="text" v-model="newContactPhoneNumber"></h5>
      <h5>Email: <input type="text" v-model="newContactEmail"></h5>
      <h5>Address: <input type="text" v-model="newContactAddress"></h5>
      <div><button v-on:click="createContact()">Create Contact</button></div>
    </div>
  <div style="padding: 40px 0 0 0;"><h1>All Contacts</h1></div>
    <div v-for="contact in contacts" style="padding: 0 0 5px 0;">
      <h2>{{ contact.first_name }} {{ contact.last_name }}</h2>
      <h3>{{ contact.phone_number }}</h3> <h4>{{ contact.email }}</h4>
      <!-- <img v-bind:src="contact.url">
      <p>Width: {{ contact.width }}</p>
      <p>Height: {{ contact.height }}</p> -->
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      contacts: [],
      newContactFirstName: "",
      newContactLastName: "",
      newContactPhoneNumber: "",
      newContactEmail: "",
      newContactAddress: ""
    };
  },
  created: function() {
    axios.get("/api/contacts").then(response => {
      this.contacts = response.data;
    });
  },
  methods: {
    createContact: function() {
      var params = {
        first_name: this.newContactFirstName,
        last_name: this.newContactLastName,
        phone_number: this.newContactPhoneNumber,
        email: this.newContactEmail,
        address: this.newContactAddress
      };
      axios.post("/api/contacts", params).then(response => {
        this.Contacts.push(response.data);
        this.newContactFirstName = "";
        this.newContactLastName = "";
        this.newContactPhoneNumber = "";
        this.newContactEmail = "";
        this.newContactAddress = "";
      });
    }

  }
};
</script>