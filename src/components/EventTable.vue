<template>
  <div id="event-table" class="small-container">
    <p
      v-if="events.length < 1"
      class="empty-table"
    >
      No events
    </p>
    <table v-else>
      <thead>
        <tr>
          <th>Event</th>
          <th>Description</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr
          :key="event.id"
          v-for="event in events"
        >
          <td v-if="editing === event.id">
            <input
              type="text"
              v-model="event.name"
            >
          </td>
          <td v-else>{{event.name}}</td>
          <td v-if="editing === event.id">
            <input
              type="text"
              v-model="event.body"
            >
          </td>
          <td v-else>{{event.body}}</td>
          <td v-if="editing === event.id">
            
            <button
              class="muted-button"
              @click="editing = null"
            >DONE</button>
          </td>
          <td v-else>
            <button class="white" @click="editMode(event.id)">EDIT</button>
            <button class="red" @click="$emit('delete:event', event.id)">DELETE</button>
          </td>

        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'event-table',
  props: {
    events: Array,
  },
  data() {
    return {
      editing: null,
    }
  },
  methods: {
    editMode(id) {
      this.editing = id
    },

    editEvent(event) {
      if (event.name === '' || event.body === '') return
      this.$emit('edit:event', event.id, event)
      this.editing = null
    }
  }
}
</script>

<style scoped>


.red {
  background-color: red; 
  width: 100px; height: 50px;
}

.green {
  background-color: white;
  color: black;
  width: 100px; height: 50px;
}

.muted-button{
  background-color: rgb(137, 162, 137); 
  width: 100px; height: 50px;
}
  .red {
  background-color: red; 
  width: 100px; height: 50px;
}

.white {
  background-color: green;
  width: 100px; height: 50px;
}

input {
  margin: 0;
}

.empty-table {
  text-align: center;
}
</style>
