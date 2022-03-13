<script>
name: "Home";

export default {
  components: {},
  methods: {
    async fetchCovidApi() {
      const covidApi = await fetch("https://api.covid19api.com/summary");
      const data = covidApi.json();
      return data;
    },
  },
  // This will automatically run once the page open
  async created(){
    const data = await this.fetchCovidApi()
    console.log(data)
  }
};
</script>

<template>
  <main class="text-center">Hello Home</main>
</template>
