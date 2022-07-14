<template>
  <div :class="containerClass">
    <label :for="uuidProp"
           class="form-label text-start w-100"
           v-text="label"></label>
    <input :type="inputType"
           class="form-control"
           :id="uuidProp"
           :name="name"
           :placeholder="placeholder"
           v-model="inputData">
  </div>
</template>

<script>
export default {
  name: "FormInput",
  props: {
    inputType: {
      default: "text",
      type: String
    },
    uuid: String,
    column: {
      default: 12,
      type: Number
    },
    label: String,
    name: String,
    placeholder: String,
    validation: {
      default: () => { return {}},
      type: Object
    },
    value: {
      type: [String, Number]
    }
  },
  data() {
    return {
      uuidGenerate: this.uuidv4()
    }
  },
  computed: {
    uuidProp() {
      return this.uuid ? this.uuid : this.uuidGenerate
    },
    containerClass() {
      return [
          'mb-3',
          'col-md-'+this.column
      ]
    },
    inputData: {
      get() { return this.value },
      set(d) { this.$emit('input', d) }
    }
  },
  methods: {
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