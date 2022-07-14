<template>
  <div :class="containerClass">
    <label :for="uuid"
           class="form-label text-start w-100"
           v-text="label"></label>
    <textarea class="form-control"
              :id="uuid"
              :name="name"
              :rows="textareaRows"
              :placeholder="placeholder"
              v-model="inputData"></textarea>
  </div>
</template>

<script>
export default {
  name: "FormTextarea",
  props: {
    uuid: String,
    column: {
      default: 12,
      type: Number
    },
    textareaRows: {
      default: 5,
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