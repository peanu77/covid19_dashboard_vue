<template>
  <main v-if="!loading">
    <DataTitle :text="title" :dataData="dataDate" />
    <CountrySelect @get-country="getCountryData" :countries="countries" />
    <DataBoxes :stats="stats" />
    <button @click="clearCountryData" v-if="stats.Country"

      class="
        bg-orange-300
        text-white
        rounded
        p-3
        mt-10
        focus:outline-none
        hover:bg-green-600
      "
    >
      Clear Country
    </button>
  </main>
  <main class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-gray-500 text-3xl mt-10 mb-6">Fetching Data</div>
    <img :src="loadingImage" class="w-24 m-auto" alt="hourglass" />
  </main>
</template>
<script>
import DataTitle from "../components/DataTitle.vue";
import DataBoxes from "../components/DataBoxes.vue";
import CountrySelect from "../components/ContrySelect.vue";

export default {
  name: "Home",

  components: {
    DataTitle,
    DataBoxes,
    CountrySelect,
  },
  methods: {
    // Fetch A
    async fetchCovidApi() {
      const covidApi = await fetch("https://api.covid19api.com/summary");
      const data = covidApi.json();
      return data;
    },
    getCountryData(country) {
      this.stats = country;
      this.title = country.Country;
    },
    async clearCountryData(){
      this.loading = true
      const data = await this.fetchCovidApi()
      this.title = 'Global'
      this.loading =false
    }
  },
  data() {
    return {
      loading: true,
      title: "Global",
      dataDate: "",
      stats: {},
      countries: [],
      // TODO : Use this later
      loadingImage: "../assets/hourglass.gif",
    };
  },
  // This will automatically run once the page open
  async created() {
    const data = await this.fetchCovidApi();
    this.dataDate = data.Date;
    this.stats = data.Global;
    this.countries = data.Countries;
    this.loading = false;
    
  },
};
</script>

<style>
</style>