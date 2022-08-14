<template>
  <div id="event-form" class="small-container">
    <form @submit.prevent="handleSubmit">
      <label>Event Type</label>
      <input
        ref="first"
        type="text"
        :class="{ 'has-error': submitting && invalidName }"
        v-model="event.name"
        @focus="clearStatus"
        @keypress="clearStatus"
      >
      <label>Description</label>
      <input
        type="text"
        :class="{ 'has-error': submitting && invalidBody }"
        v-model="event.body"
        @focus="clearStatus"
      >
      <p v-if="error && submitting" class="error-message">❗Please fill out all required fields</p>
      <p v-if="success" class="success-message">✅ Event successfully added</p>
      <button>ADD EVENT</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "event-form",
  data() {
    return {
      error: false,
      submitting: false,
      success: false,
      event: {
        name: "",
        body: ""
      }
    };
  },
  computed: {
    invalidName() {
      return this.event.name === "";
    },

    invalidBody() {
      return this.event.body === "";
    }
  },
  methods: {
    handleSubmit() {
      this.clearStatus();
      this.submitting = true;

      if (this.invalidEvent || this.invalidBody) {
        this.error = true;
        return;
      }

      this.$emit("add:event", this.event);
      this.$refs.first.focus();
      this.event = {
        event: "",
        body: ""
      };
      this.clearStatus();
      this.submitting = false;
    },

    clearStatus() {
      this.success = false;
      this.error = false;
    }
  }
};
</script>

<style scoped>
form {
  margin-bottom: 2rem;
}

[class*="-message"] {
  font-weight: 500;
}

.error-message {
  color: #d33c40;
}

.success-message {
  color: #32a95d;
}
</style>
