<template>
  <div class="flex-row text-center">
    <input
      v-for="i in 6"
      :id="`input${i}`"
      :key="i"
      :ref="`input${i}`"
      v-model="inputValue[i - 1]"
      :class="`border p-3 rounded mb-4 w-12 m-0.5 text-center border-${borderColor}-500`"
      maxlength="1"
      @input="onInput"
      @paste="onPaste"
      @paste.prevent
    />
    <p>{{ message }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      borderColor: 'lightgray',
      inputValue: [],
      message: '',
    }
  },
  mounted() {
    // By default, the first digit has focus
    this.focusDigit(1)
  },
  methods: {
    onInput(event) {
      const digit = Number(event.target.id.slice(-1))
      if (digit < 6) {
        // Switch to next digit on input
        this.focusDigit(digit + 1)
      }
      this.inputValue[digit - 1] = Number(event.data)
      this.verify()
    },
    onPaste(event) {
      // Handles the scenario where the user pastes the code directly
      const pastedText = event.clipboardData.getData('text/plain')
      const pastedTextArray = Array.from(pastedText, Number)
      this.inputValue = pastedTextArray
      this.verify()
    },
    focusDigit(el) {
      this.$refs[`input${el}`][0].focus()
    },
    verify() {
      if (this.inputValue.length > 5) {
        // Hardcoded correct code to check
        if (this.inputValue.join('') === '123456') {
          this.borderColor = 'green'
          // A cookie is set for basic (fake) auth policy
          this.$cookies.set('authenticated', 'true')
          this.message = 'Success!'
          this.$router.push('/')
        } else {
          // Invalid code
          this.borderColor = 'red'
          this.focusDigit(1)
          this.message = 'Invalid code, try again!'
          this.inputValue = []
        }
      }
    },
  },
}
</script>