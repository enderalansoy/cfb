<template>
  <div class="grid grid-cols-12">
    <nuxt-link class="col-span-11" to="/">
      <div class="font-bold text-xl mb-2">{{ title }}</div>
    </nuxt-link>
    <div>
      <button
        class="
          w-full
          bg-green-300
          hover:bg-green-500
          text-white
          py-1
          px-2
          rounded
          text-center
        "
        @click="onClick"
      >
        Log out
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    title: String,
  },
  methods: {
    onClick() {
      // Log out button removes the cookie
      this.$cookies.removeAll()
      location.reload()
    },
  },
}
</script>
