<template>
  <div class="container my-12 mx-auto px-3 md:px-6">
    <Header title="CFB database" />
    <div>
      <input
        type="search"
        v-model="search"
        class="block border border-grey-light w-full p-3 rounded mb-4"
        placeholder="Search a team by name"
      />
    </div>
    <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-5">
      <div class="m-2" v-for="team in pages[currentPage]" :key="team.id">
        <team-card :team="team" />
      </div>
    </div>
    <div class="container flex justify-center mx-auto m-6">
      <pagination
        :current-page="currentPage"
        :pages="pages"
        @select-page="selectPage"
      />
    </div>
  </div>
</template>

<script>
import Header from './Header'
import TeamCard from './Team/TeamCard'

export default {
  components: { TeamCard, Header },
  data() {
    return {
      search: '',
      currentPage: 0,
    }
  },
  props: {
    teams: {
      type: Array,
      default() {
        return []
      },
    },
  },
  computed: {
    searchedTeams() {
      return this.teams.teams.filter((team) => {
        return team.school.toLowerCase().includes(this.search.toLowerCase())
      })
    },
    pages() {
      const perChunk = 10
      return this.searchedTeams.reduce((resultArray, item, index) => {
        const chunkIndex = Math.floor(index / perChunk)

        if (!resultArray[chunkIndex]) {
          resultArray[chunkIndex] = [] // start a new chunk
        }

        resultArray[chunkIndex].push(item)

        return resultArray
      }, [])
    },
  },
  watch: {
    search() {
      this.currentPage = 0
    },
  },
  methods: {
    selectPage(page) {
      this.currentPage = page
    },
  },
}
</script>
