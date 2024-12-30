<template>
  <div>
    <h2>Liste des Lancements</h2>
    <select v-model="filter" @change="fetchLaunches">
      <option value="all">Tous les lancements</option>
      <option value="success">Lancements réussis</option>
      <option value="failed">Lancements échoués</option>
    </select>
    <div v-if="launches.length">
      <div v-for="launch in launches" :key="launch.id" class="launch">
        <h3>{{ launch.name }}</h3>
        <p>Date : {{ formatDate(launch.date_utc) }}</p>
        <p>{{ launch.details }}</p>
        <img :src="launch.links.patch.small" alt="Patch" />
        <a :href="launch.links.article" target="_blank">Lire l'article</a>
        <button @click="showVideo(launch.links.youtube_id)">Voir la vidéo</button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      launches: [],
      filter: 'all',
    };
  },
  methods: {
    fetchLaunches() {
      axios.get('https://api.spacexdata.com/v4/launches')
        .then(response => {
          let launches = response.data;
          if (this.filter === 'success') {
            launches = launches.filter(launch => launch.success === true);
          } else if (this.filter === 'failed') {
            launches = launches.filter(launch => launch.success === false);
          }
          this.launches = launches.slice(0, 10); // Limiter aux 10 derniers
        });
    },
    formatDate(date) {
      const d = new Date(date);
      return d.toLocaleDateString('fr-FR');
    },
    showVideo(youtubeId) {
      const url = `https://www.youtube.com/watch?v=${youtubeId}`;
      window.open(url, '_blank');
    },
  },
  mounted() {
    this.fetchLaunches();
  },
};
</script>

<style scoped>
.launch {
  border: 1px solid #ccc;
  margin: 10px;
  padding: 10px;
}
</style>
