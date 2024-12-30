<template>
  <div class="launch-card border rounded-md p-4 mb-4 bg-white shadow">
    <h3 class="text-xl font-bold">{{ launch.name }}</h3>
    <p><strong>Date :</strong> {{ formattedDate }}</p>
    <p><strong>Détails :</strong> {{ launch.details || 'Non disponible' }}</p>
    <img :src="launch.links.patch.small" alt="Image mission" class="w-32 h-32 mt-2" />
    <a
      :href="launch.links.article"
      target="_blank"
      class="text-blue-500 underline mt-2 inline-block"
    >En savoir plus</a>
    <button
      @click="showVideo"
      class="bg-blue-500 text-white px-4 py-2 rounded mt-2"
    >Voir la vidéo</button>
  </div>
</template>

<script>
export default {
  props: ['launch'],
  methods: {
    showVideo() {
      window.open(this.launch.links.webcast, '_blank');
    },
  },
  computed: {
    formattedDate() {
      return new Date(this.launch.date_utc).toLocaleDateString();
    },
  },
};
</script>
