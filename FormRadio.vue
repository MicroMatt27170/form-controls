<template>
  <div :class="containerClass">
    <label :for="uuid"
           class="form-label text-start w-100"
           v-text="label"></label>

    <div :class="formCheckClass"
         v-for="(radio, k) in selectOptions"
         :key="radio.value">
      <input type="radio"
             class="form-check-input"
             :name="name"
             :value="radio.value"
             :id="getUuidForRadio(k, radio.value)"
             v-model="inputData">
      <label class="form-check-label"
             :for="getUuidForRadio(k, radio.value)"
             v-text="radio.value"></label>
    </div>
  </div>
</template>

<script>
export default {
  name: "FormRadio",
  props: {
    value: {
      type: [String, Number]
    },
    uuid: String,
    column: {
      default: 12,
      type: Number
    },
    label: String,
    name: String,
    radioInline: {
      default: false,
      type: Boolean
    },
    selectOptions: Array,
    validation: Array
  },
  data() {
    return {
      radioUuid: this.uuidv4()
    }
  },
  computed: {
    containerClass() {
      return [
        'mb-3',
        'col-md-'+this.column
      ]
    },
    inputData: {
      get() { return this.value },
      set(d) { this.$emit('input', d) }
    },
    formCheckClass() {
      return [
          'form-check',
          this.radioInline ? 'form-check-inline' : ''
      ]
    }
  },
  methods: {
    getUuidForRadio(key, value) {
      return this.radioUuid + '-' + key + '-' + value
    },
    uuidv4() {
      return ([1e7]+-1e3+-4e3+-8e3+-1e11).replace(/[018]/g, c =>
        (c ^ crypto.getRandomValues(new Uint8Array(1))[0] & 15 >> c / 4).toString(16)
      );
    }
  }
}
</script>

<style scoped>

</style>