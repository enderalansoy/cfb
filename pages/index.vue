<template>
  <div>
    <home :teams="{ teams }" />
  </div>
</template>

<script>
export default {
  middleware({ app, redirect }) {
    // Middleware to check if the cookie is set
    if (!app.$cookies.get('authenticated')) {
      return redirect('/login')
    }
  },
  async asyncData({ $axios }) {
    $axios.setToken(
      'dpWo1w4gqv/puBqEXCuHoN3GyzlZuA403nQJ9Po29CqDam3dVcSLsOFBEWlFRSpw',
      'Bearer'
    )
    const teams = await $axios.get('/api-teams')
    return { teams: teams.data }
  },
}
</script>
