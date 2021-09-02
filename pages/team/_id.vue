<template>
  <team-details
    :id="{ id }"
    :team="{ team }"
    :games="{ games }"
    :games-past="{ gamesPast }"
  />
</template>

<script>
import TeamDetails from '../../components/Team/TeamDetails'

export default {
  components: {
    TeamDetails,
  },
  props: {
    id: {
      type: String,
      default: '',
    },
  },
  async asyncData({ route, $axios }) {
    // Default year for past game results is 2020
    const year = route.query.year || '2020'

    $axios.setToken(
      'dpWo1w4gqv/puBqEXCuHoN3GyzlZuA403nQJ9Po29CqDam3dVcSLsOFBEWlFRSpw',
      'Bearer'
    )

    const teams = await $axios.get('/api-teams')

    const team = teams.data.find(
      (t) => t.school === route.params.id.replace('-', ' ')
    )

    const gamesCurrent = await $axios.get(
      `/api-games?team=${team.school}&year=2021`
    )

    const gamesPast = await $axios.get(
      `/api-games?team=${team.school}&year=${year}`
    )

    return { team, games: gamesCurrent.data, gamesPast: gamesPast.data }
  },
}
</script>
