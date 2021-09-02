<template>
  <div class="max-w-sm rounded shadow-lg p-2 h-full flex-1 m-2">
    <div class="font-bold text-xl mb-2 text-center">
      <select v-model="year" @change="dateSelected">
        <option v-for="i in yearsList" :key="i">{{ i }}</option>
      </select>
      Schedule
    </div>
    <div
      v-for="game in games"
      :key="game.id"
      class="rounded border p-2 h-full flex-row m-2 hover:bg-green-100"
    >
      <nuxt-link :to="`/game/${game.id}`">
        <p v-if="game.home_points" class="text-gray-700 font-bold">
          Week {{ game.week }}: {{ game.away_team }} {{ game.away_points }} @
          {{ game.home_team }} {{ game.home_points }}
        </p>
        <p v-else class="text-gray-700 font-bold">
          Week {{ game.week }}: {{ game.away_team }} {{ game.away_points }} @
          {{ game.home_team }} {{ game.home_points }}
        </p>
        <p class="text-gray-700">{{ parseDate(game.start_date) }}</p>
      </nuxt-link>
    </div>
  </div>
</template>

<script>
import { DateTime } from 'luxon'

export default {
  props: {
    games: {
      type: Array,
      default() {
        return []
      }
    },
  },
  data() {
    return {
      // Default year for a schedule is 2020
      year: this.$route?.query?.year || '2020',
    }
  },
  computed: {
    yearsList() {
      // Gets a list of years for the dropdown
      const max = new Date().getFullYear() - 1
      const min = max - 9
      const years = []

      for (let i = max; i >= min; i -= 1) {
        years.push(i)
      }
      return years
    },
  },
  watch: {
    // To induce a reload on a query param change
    $route(to, from) {
      if (to !== from) {
        location.reload()
      }
    },
  },
  methods: {
    parseDate(date) {
      return DateTime.fromISO(date).toFormat('ff')
    },
    dateSelected(event) {
      this.$router.push(`?year=${event.target.value}`)
    },
  },
}
</script>