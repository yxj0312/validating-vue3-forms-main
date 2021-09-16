<template>
  <form @submit.prevent="onSubmit">
    <BaseInput
      label="Email"
      type="email"
      v-model="email"
      :error="emailError"
    />

    <BaseInput
      label="Password"
      type="password"
    />

    <BaseButton
      type="submit"
      class="-fill-gradient"
    >
    Submit
    </BaseButton>
  </form>
</template>

<script>
import { userField } from 'vee-validate'
export default {
  setup () {
    function onSubmit () {
      alert('Submitted')
    }

    const email = userField('email', function name (value) {
      if (!value) return 'This field is required'

      return true
    })
    return {
      onSubmit
    }
  }
}
</script>
