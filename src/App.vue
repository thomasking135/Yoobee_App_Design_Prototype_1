/* eslint-disable */
<template>
  <div id="app" class="small-container">
    <a href="#app"><img src="./assets/logo.png" alt="logo"/></a>
    
    <ul class="text-align">
      <a href="#about">ABOUT</a>&emsp;
      <a href="#register-login">REGISTER/LOGIN</a>&emsp;
      <a href="#logoff">LOGOFF</a>

      
  </ul>
    <hr>
    <h1>Welcome</h1>
    <div v-if="login">
    <p class="center">You are logged in to Hap!</p>
    </div>
    <event-form @add:event="addEvent"/>
    <event-table
      :events="events"
      @delete:event="deleteEvent"
      @edit:event="editEvent"
    />
   <h1 id="about">About</h1>
<p>Welcome to Hap app. An app where you can find and share events
  in your community. Simply browse the events created by others or post 
  up your own. Whatever your event, it's happening on Hap!</p>
  <br>
  <img class="costume" src="./assets/costumeParty.jpg" alt="logo"/>
  <br>


<a class="text-align" href="#app">HOME</a>
  </div>
  
  
</template>

<script>

import EventTable from "@/components/EventTable.vue";
import EventForm from "@/components/EventForm.vue";



export default {
  name: "app",
  components: {
    EventTable,
    EventForm
 
},
  data() {
    return {
      events: [],
      login: true,
    };
  },

  mounted() {
    this.getEvents();
  },

  methods: {
    async getEvents() {
      try {
        const response = await fetch(
          "https://jsonplaceholder.typicode.com/comments"
        );
        const data = await response.json();
        this.events = data;
      } catch (error) {
        console.error(error);
      }
    },

    async addEvent(event) {
      try {
        const response = await fetch(
          "https://jsonplaceholder.typicode.com/comments",
          {
            method: "POST",
            body: JSON.stringify(event),
            headers: { "Content-type": "application/json; charset=UTF-8" }
          }
        );
        const data = await response.json();
        this.events = [...this.events, data];
      } catch (error) {
        console.error(error);
      }
    },

    async editEvent(id, updatedEvent) {
      try {
        const response = await fetch(
          `https://jsonplaceholder.typicode.com/comments/${id}`,
          {
            method: "PUT",
            body: JSON.stringify(updatedEvent),
            headers: { "Content-type": "application/json; charset=UTF-8" }
          }
        );
        const data = await response.json();
        this.events = this.events.map(event =>
          event.id === id ? data : event
        );
      } catch (error) {
        console.error(error);
      }
    },

    async deleteEvent(id) {
      try {
        await fetch(`https://jsonplaceholder.typicode.com/comments/${id}`, {
          method: "DELETE"
        });
        this.events = this.events.filter(event => event.id !== id);
      } catch (error) {
        console.error(error);
      }
    }
  }
};
</script>

<style>
button {
  background: #009435;
  border: 1px solid #009435;
}

button:hover,
button:active,
button:focus {
  background: #32a95d;
  border: 1px solid #32a95d;
}

.center{
  text-align: center;
}

.small-container {
  max-width: 680px;
}

h1 {
  text-align: center;
}

.text-align{
  font-weight: bold;
  font-size: 25px;
  text-align: center;
}

.costume {
  width: 100%;
}
</style>
