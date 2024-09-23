<template>
  <div>
    <h1>COVID-19 Dashboard Clone</h1>
    <WorldwideStats />
    <NeighborStats />
    <client-only>
      <CovidMap />
    </client-only>
  </div>
</template>

<script>
export default {
  components: {
    CovidMap: () => import('@/components/CovidMap.vue'),
    WorldwideStats: () => import('~/components/NeighborStats.vue'),
    NeighborStats: () => import('~/components/WorldwideStats.vue')
  }
}
</script>

<style scoped>
h1 {
  text-align: center;
  margin-bottom: 20px;
}
</style>