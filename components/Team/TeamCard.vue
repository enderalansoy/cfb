<template>
  <nuxt-link :to="`/team/${this.team.school.replace(' ', '-')}`">
    <div
      class="
        max-w-sm
        rounded
        overflow-hidden
        shadow-lg
        p-2
        h-full
        cursor-pointer
        hover:bg-green-200
      "
    >
      <img class="w-full" :src="team.logos[0]" alt="Team logo" />
      <div class="px-6 py-4">
        <div class="font-bold text-xl mb-2">{{ team.school }}</div>
        <p class="text-gray-700 text-base">
          {{ team.location.city }}, {{ team.location.state }}
        </p>
      </div>
      <div class="px-6 pt-4 pb-2">
        <span
          v-if="team.conference"
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
          {{ team.conference }}
        </span>
        <span
          v-if="team.division"
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
          {{ team.division }}
        </span>
      </div>
    </div>
  </nuxt-link>
</template>

<script>
export default {
  props: {
    team: {},
  },
}
</script>
