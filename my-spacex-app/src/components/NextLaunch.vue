<template>
  <div class="next-launch">
    <h2>Prochain Lancement</h2>
    <div v-if="launch">
      <h3>{{ launch.name }}</h3>
      <p>Date : {{ formattedDate }}</p>
      <p>Décompte : {{ countdown }} secondes</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      launch: null,
      countdown: null,
    };
  },
  computed: {
    formattedDate() {
      if (this.launch) {
        const date = new Date(this.launch.date_utc);
        return date.toLocaleDateString('fr-FR');
      }
      return '';
    },
  },
  methods: {
    fetchNextLaunch() {
      axios.get(' https://api.spacexdata.com/v5/launches/latest')
        .then(response => {
          this.launch = response.data;
          this.updateCountdown();
        });
    },
    updateCountdown() {
      if (this.launch) {
        const launchDate = new Date(this.launch.date_utc).getTime();
        this.countdown = Math.floor((launchDate - Date.now()) / 1000);
        setInterval(() => {
          this.countdown = Math.max(0, Math.floor((launchDate - Date.now()) / 1000));
        }, 1000);
      }
    },
  },
  mounted() {
    this.fetchNextLaunch();
  },
};
</script>

<style scoped>
.next-launch {
  text-align: center;
}
</style>
