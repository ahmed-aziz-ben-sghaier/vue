<template>
  <div id="app">
    <h1>SpaceX Launches</h1>
    <NextLaunch />
    <LaunchList />
  </div>
</template>

<script>
import NextLaunch from './components/NextLaunch.vue';
import LaunchList from './components/LaunchList.vue';

export default {
  components: {
    NextLaunch,
    LaunchList,
  },
};
</script>
