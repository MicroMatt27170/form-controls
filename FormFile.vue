<template>
  <div :class="containerClass">
    <label :for="uuid" class="form-label" v-text="label"></label>
    <input class="form-control"
           @change="onChangeFile"
           type="file"
           :id="uuid"
           :multiple="isArray"
           :name="name">
  </div>
</template>

<script>
export default {
  name: "FormFile",
  props: {
    uuid: String,
    column: {
      default: 12,
      type: Number
    },
    label: String,
    name: String,
    isArray: {
      default: false,
      type: Boolean
    },
    validation: {
      default: () => { return {}},
      type: Object
    },
    value: {
      type: [Object, Array]
    }
  },
  data() {
    return {

    }
  },
  computed: {
    containerClass() {
      return [
        'mb-3',
        'col-md-'+this.column
      ]
    }
  },
  methods: {
    onChangeFile(event) {
      let fs = event.target.files;
      fs = this.isArray ? fs : fs.length > 0 ? fs[0] : null;
      console.log('file change', fs)
      this.$emit('input', fs)
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