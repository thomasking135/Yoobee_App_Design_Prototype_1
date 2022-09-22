<template>
<div id="about" class="container">
  <h1>About</h1>
<p>Welcome to Hap app. An app where you can find and share events
  in your community. Simply browse the events created by others or post 
  up your own. Whatever your event, it's happening on Hap!</p>
  <br>
  <img class="costume" src="../assets/costumeParty.jpg" alt="logo"/>
  <button @click="increment">Like Us? {{ count }}</button>
  <br>
</div>


<a class="text-align" href="#app">HOME</a>

</template>

<script>
  export default {
    name: 'about-page',
    data() {
    return {
      count: 0
    };
  },

  methods: {
    increment() {
      this.count++;
    }
  },

  // Lifecycle hooks are called at different stages
  // of a component's lifecycle.
  // This function will be called when the component is mounted.
  mounted() {
    console.log(`The initial count is ${this.count}.`);
  }
};
  
</script>

<style>
.costume {
  width: 100%;
}

.text-align {
  font-weight: bold;
  font-size: 25px;
  text-align: center;
}
</style>