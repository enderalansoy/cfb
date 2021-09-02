<template>
  <div class="container my-12 mx-auto px-6 md:px-12 flex">
    <div class="max-w-sm rounded shadow-lg p-2 h-full flex-1 m-2">
      <img class="w-full" :src="team.team.logos[0]" alt="Team logo" />
      <div class="p-4">
        <div class="font-bold text-xl mb-2">{{ team.team.school }}</div>
        <p class="text-gray-700 text-base">
          Location: {{ team.team.location.city }},
          {{ team.team.location.state }}
        </p>
        <p class="text-gray-700 text-base">
          Mascot: {{ team.team.mascot || 'N/A' }}
        </p>
        <p class="text-gray-700 text-base">
          Abbrevation: {{ team.team.abbrevation || 'N/A' }}
        </p>
      </div>
      <div class="px-6 pt-4 pb-2">
        <span
          v-if="team.team.conference"
          class="
            inline-block
            bg-gray-200
            rounded-full
            px-3
            py-1
            text-sm
            font-semibold
            text-gray-700
            mr-2
            mb-2
          "
        >
          {{ team.team.conference }}
        </span>
        <span
          v-if="team.team.division"
          class="
            inline-block
            bg-gray-200
            rounded-full
            px-3
            py-1
            text-sm
            font-semibold
            text-gray-700
            mr-2
            mb-2
          "
        >
          {{ team.team.division }}
        </span>
      </div>
    </div>
    <div class="max-w-sm rounded shadow-lg p-2 h-full flex-1 m-2">
      <div class="font-bold text-xl mb-2 text-center">Current Schedule</div>
      <div
        v-for="game in games.games"
        :key="game.id"
        class="rounded border p-2 h-full flex-row m-2"
      >
        <p class="text-gray-700 font-bold">
          Week {{ game.week }} - {{ game.away_team }} @ {{ game.home_team }}
        </p>
        <p class="text-gray-700">{{ parseDate(game.start_date) }}</p>
      </div>
    </div>
    <schedule :games="gamesPast.gamesPast" />
  </div>
</template>

<script>
import { DateTime } from 'luxon'
import Schedule from '../Team/Schedule'

export default {
  components: {
    Schedule,
  },
  props: {
    team: {
      type: Object,
      default() {
        return {}
      },
    },
    games: {
      type: Object,
      default() {
        return {}
      },
    },
    gamesPast: {
      type: Object,
      default() {
        return {}
      },
    },
  },
  methods: {
    parseDate(date) {
      return DateTime.fromISO(date).toFormat('ff')
    },
  },
}
</script>
