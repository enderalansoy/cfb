<template>
  <div class="min-h-screen flex flex-col">
    <div
      class="
        container
        max-w-sm
        mx-auto
        flex-1 flex flex-col
        items-center
        justify-center
        px-2
      "
    >
      <div class="px-6 py-8 rounded shadow-md text-black w-full">
        <h1 class="mb-8 text-3xl text-center">Login</h1>
        <div v-if="!submitClicked">
          <input
            type="email"
            class="block border border-grey-light w-full p-3 rounded mb-4"
            placeholder="Enter your email"
          />
          <button
            class="
              w-full
              bg-green-300
              hover:bg-green-500
              text-white
              py-2
              px-4
              rounded
              text-center
            "
            @click="onSubmit"
          >
            Send code
          </button>
        </div>
        <div v-else>
          <verify />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Verify from '../../components/Login/Verify'

export default {
  components: {
    Verify,
  },
  data() {
    return {
      submitClicked: false,
    }
  },
  methods: {
    onSubmit() {
      this.submitClicked = true
    },
  },
}
</script>
