<template>
  <div class="country-stats">
    <h2>Indonesia's Neighbor Statistics</h2>
    <table>
      <thead>
      <tr>
        <th>Country</th>
        <th>Total Cases</th>
        <th>Total Deaths</th>
        <th>Total Recovered</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="country in countriesData" :key="country.name">
        <td><b v-if="country.country === 'Indonesia'">{{ country.country }}</b><div v-else>{{ country.country }}</div></td>
        <td><b v-if="country.country === 'Indonesia'">{{ country.cases }}</b><div v-else>{{ country.cases }}</div></td>
        <td><b v-if="country.country === 'Indonesia'">{{ country.deaths }}</b><div v-else>{{ country.deaths }}</div></td>
        <td><b v-if="country.country === 'Indonesia'">{{ country.recovered }}</b><div v-else>{{ country.recovered }}</div></td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      listCountries: ['Indonesia', 'Singapore', 'Malaysia', 'Philippines', 'Australia', 'Thailand'],
      countriesData: [],
    };
  },
  mounted() {
    this.listCountries.forEach(country => {
      fetch(`https://disease.sh/v3/covid-19/countries/${country}`)
        .then(response => response.json())
        .then(data => {
          this.countriesData.push(data);
        })
        .catch(error => {
          console.error(`Error fetching ${country} data:`, error);
        });
    });
  }
}
</script>

<style scoped>
.country-stats {
  text-align: center;
  margin: 20px;
}

table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  padding: 10px;
  border: 1px solid #ddd;
}

th {
  background-color: #f4f4f4;
}
</style>