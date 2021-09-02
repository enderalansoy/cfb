<template>
  <ul class="flex">
    <li>
      <button
        class="h-10 px-5 text-gray-600 bg-white hover:bg-gray-100 rounded"
        :disabled="currentPage === 0"
        @click="select(currentPage - 1)"
      >
        Prev
      </button>
    </li>
    <li v-for="(page, i) in pages" :key="i">
      <button
        class="h-10 px-5 rounded hover:bg-gray-100"
        :class="{
          'text-white bg-gray-600 hover:bg-gray-600': currentPage === i,
        }"
        @click="select(i)"
      >
        {{ i + 1 }}
      </button>
    </li>
    <li>
      <button
        class="h-10 px-5 text-gray-600 bg-white hover:bg-gray-100 rounded"
        :disabled="currentPage === pages.length"
        @click="select(currentPage + 1)"
      >
        Next
      </button>
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    currentPage: {
      type: Number,
      default: 0,
    },
    pages: {
      type: Array,
      default() {
        return []
      },
    },
  },
  methods: {
    select(page) {
      // Induce the selectPage action on parent
      this.$emit('select-page', page)
    },
  },
}
</script>