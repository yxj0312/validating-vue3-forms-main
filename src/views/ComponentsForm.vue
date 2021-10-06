<template>
  <div>
    <h1>Create an Event</h1>
    <form>
      <BaseSelect
        label="Select a category"
        :options="categories"
        v-model=""
        :error=""
      />

      <h3>Name & describe your event</h3>
      <BaseInput
        label="Title"
        v-model=""
        :error=""
        type="text"
      />

      <BaseInput
        label="Description"
        v-model=""
        :error=""
        type="text"
      />

      <h3>Where is your event?</h3>
      <BaseInput
        label="Location"
        v-model=""
        :error=""
        type="text"
      />

      <h3>Are pets allowed?</h3>
      <BaseRadioGroup
        v-model=""
        :error=""
        name="pets"
        :options="[
          { value: 1, label: 'Yes' },
          { value: 0, label: 'No' }
        ]"
      />

      <h3>Extras</h3>
      <div>
        <BaseCheckbox
          label="Catering"
          v-model=""
          :error=""
        />
      </div>

      <div>
        <BaseCheckbox
          label="Live music"
          v-model=""
          :error=""
        />
      </div>

      <div>
        <BaseButton
          type="submit"
          class="-fill-gradient"
          something="else"
        >
          Submit
        </BaseButton>
      </div>
    </form>
  </div>
</template>

<script>
import { useField, useForm } from 'vee-validate'
export default {
  setup () {
    const required = value => {
      const requiredMessage = 'This field is required'
      if (value === undefined || value === null) return requiredMessage
      if (!String(value).length) return requiredMessage
      return true
    }
    const minLength = (number, value) => {
      if (String(value).length < number) return 'Please type at least ' + number + ' characters'
      return true
    }
    const anything = () => {
      return true
    }

    const validationSchema = {
      category: required,
      title: value => {
        const req = required(value)
        if (req !== true) return req
        const min = minLength(3, value)
        if (min !== true) return min
        return true
      },
      description: required,
      location: undefined,
      pets: anything,
      catering: anything,
      music: anything
    }

    useForm({
      validationSchema
    })

    const { value: category } = useField('category')
    const { value: title } = useField('title')
    const { value: description } = useField('description')
    const { value: location } = useField('location')
    const { value: pets } = useField('pets')
    const { value: catering } = useField('catering')
    const { value: music } = useField('music')
    return {}
  }
}
</script>
