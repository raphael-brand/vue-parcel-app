<template>
  <div id="app">
    <!-- <HelloWorld /> -->
    <div v-if="isLoaded">
      <div v-for="showerThought in showerThoughts" :key="showerThought.data.id">
        <p class="quote">{{ showerThought.data.title }}</p>
      </div>
    </div>
  </div>
</template>

<script>
// import HelloWorld from "./components/HelloWorld";

export default {
  data() {
    return {
      isLoaded: false,
      showerThoughts: []
    };
  },
  created() {
    fetch("https://www.reddit.com/r/showerthoughts.json?limit=20")
      .then(response => response.json())
      .then(data => {
        this.showerThoughts = data.data.children;
        this.showerThoughts.shift();
        this.showerThoughts.shift();
        console.log(this.showerThoughts);
        this.isLoaded = true;
      });
  },
  components: {
    // HelloWorld
  }
};
</script>