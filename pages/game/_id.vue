<template>
  <game-details :id="{ id }" :game="{ game }" />
</template>

<script>
import GameDetails from '../../components/Game/GameDetails'

export default {
  components: {
    GameDetails,
  },
  props: {
    id: {
      type: String,
      default: '',
    },
  },
  async asyncData({ route, $axios }) {
    $axios.setToken(
      'dpWo1w4gqv/puBqEXCuHoN3GyzlZuA403nQJ9Po29CqDam3dVcSLsOFBEWlFRSpw',
      'Bearer'
    )
    const game = await $axios.get(`/api-games?id=${route.params.id}`)
    return { game: game.data }
  },
}
</script>
