<template>
  <div id="map" class="w-full h-96"></div>
</template>

<script>
import L from 'leaflet';
import 'leaflet/dist/leaflet.css';

export default {
  data() {
    return {
      listCountries: ['Singapore', 'Malaysia', 'Philippines', 'Australia', 'Thailand', 'Indonesia'],
      countriesData: [],
    };
  },
  mounted() {
    // Inisialisasi map
    this.map = L.map('map').setView([-10, 120], 3);

    // Tile layer untuk peta
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '&copy; OpenStreetMap contributors'
    }).addTo(this.map);

    // Tambahkan marker di beberapa negara
    this.listCountries.forEach(country => {
      fetch(`https://disease.sh/v3/covid-19/countries/${country}`)
          .then(response => response.json())
          .then(data => {
            L.marker([data.countryInfo.lat, data.countryInfo.long])
                .addTo(this.map)
                .bindPopup(`<img src="${data.countryInfo.flag}" style="width: 30px; height: 20px;"> <b>${data.country}</b><br>Cases: ${data.cases}<br>Deaths: ${data.deaths}<br>Recovered: ${data.recovered}`);
          })
          .catch(error => {
            console.error(`Error fetching ${country} data:`, error);
          });
    });
  }
}
</script>

<style scoped>
#map {
  width: 100%;
  height: 400px;
}
</style>