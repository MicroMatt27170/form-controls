<template>
  <div :class="containerClass">
    <input class="form-check-input"
           type="checkbox"
           :id="uuidProp"
           :name="name"
           v-model="inputData">
    <label class="form-check-label" v-text="label" :for="uuidProp"/>
  </div>
</template>

<script>
export default {
  name: "FormCheckbox",
  props: {
    uuid: String,
    label: String,
    name: String,
    column: {
      default: 12,
      type: Number
    },
    value: {
      type: Boolean
    }
  },
  data() {
    return {
      uuidGenerate: this.uuidv4()
    }
  },
  computed: {
    containerClass() {
      return [
        'mb-3',
        'form-check',
        'col-md-'+this.column
      ]
    },
    inputData: {
      get() { return this.value },
      set(d) { this.$emit('input', d) }
    },
    uuidProp() {
      return this.uuid ? this.uuid : this.uuidGenerate
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
  .form-check {
    padding-left: 2.5rem;
  }
</style>