<template>
  <div v-if="isLoaded">
    <div v-for="showerThought in showerThoughts" :key="showerThought.data.id">
      <p class="quote">{{ showerThought.data.title }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "shower-thoughts",
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
        this.isLoaded = true;
      });
  }
};
</script>

<style>
</style>