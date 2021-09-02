<template>
  <div class="container my-12 mx-auto px-6 md:px-12">
    <div class="rounded border p-2 h-full flex-row m-2">
      <div class="p-4">
        <p class="text-gray-700 text-3xl text-center">
          {{ game.game[0].home_team }}
          <span class="font-bold">{{ game.game[0].home_points }}</span> -
          <span class="font-bold">{{ game.game[0].away_points }}</span>
          {{ game.game[0].away_team }}
        </p>
      </div>
    </div>
    <div class="rounded border p-2 h-full flex-row m-2">
      <div class="p-4">
        <p class="text-gray-700 font-bold text-xl">
          Week: {{ game.game[0].week }}
        </p>
        <p class="text-gray-700">
          <span class="font-bold">Home team:</span> {{ game.game[0].home_team }}
        </p>
        <p class="text-gray-700">
          <span class="font-bold">Away team:</span> {{ game.game[0].away_team }}
        </p>
        <p class="text-gray-700">
          <span class="font-bold">Location:</span> {{ game.game[0].venue }}
        </p>
        <p class="text-gray-700">
          <span class="font-bold">Attendance:</span>
          {{ game.game[0].attendance }}
        </p>
      </div>
    </div>
    <div class="rounded border p-2 h-full flex-row m-2">
      <div class="p-4">
        <p class="text-gray-700 text-xl font-bold">Scores by quarter</p>
        <p
          v-for="i in game.game[0].home_line_scores.length"
          :key="i"
          class="text-gray-700"
        >
          <span class="font-bold">Q{{ i }}:</span> {{ game.game[0].home_team }}:
          {{ game.game[0].home_line_scores[i - 1] }} -
          {{ game.game[0].away_team }}:
          {{ game.game[0].away_line_scores[i - 1] }}
        </p>
      </div>
    </div>
    <div class="rounded border p-2 h-full flex-row m-2">
      <div class="p-4">
        <p class="text-gray-700">
          <a :href="game.game[0].highlights">See game highlights</a>
        </p>
      </div>
    </div>
    <div class="p-2 h-full m-2">
      <div class="p-4">
        <nuxt-link to="/" class="text-gray-700">Go Home</nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
import { DateTime } from 'luxon'

export default {
  props: {
    game: {
      type: Object,
      default() {
        return {}
      }
    },
  },
  methods: {
    parseDate(date) {
      return DateTime.fromISO(date).toFormat('ff')
    },
  },
}
</script>


