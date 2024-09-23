<template>
  <div class="global-stats text-center my-10">
    <h2 class="text-2xl font-bold">Worldwide Statistics</h2>
    <div class="stat grid grid-cols-1 md:grid-cols-3 gap-4">
      <p>Total Cases: <span class="font-semibold">{{ globalData.cases || noData }}</span></p>
      <p>Total Deaths: <span class="font-semibold">{{ globalData.deaths || noData }}</span></p>
      <p>Total Recovered: <span class="font-semibold">{{ globalData.recovered || noData }}</span></p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      globalData: {},
      noData: 'N/A'
    };
  },
  mounted() {
    fetch('https://disease.sh/v3/covid-19/all')
        .then(response => response.json())
        .then(data => {
          this.globalData = data;
        })
        .catch(error => {
          console.error('Error fetching global data:', error);
        });
  }
}
</script>

<style scoped>
.global-stats {
  text-align: center;
  margin: 20px 0;
}

.stat p {
  font-size: 1.2rem;
  margin: 5px 0;
}
</style>