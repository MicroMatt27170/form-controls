<template>
  <div :class="containerClass">
    <label :for="uuid"
           class="form-label text-start w-100"
           v-text="label"></label>
    <select class="form-control"
            v-if="isVanilla"
            :id="uuid"
            :name="name"
            v-model="inputData">
      <option v-for="opt in selectOptions"
              :key="opt.value"
              :value="opt.value"
              v-text="opt.text"></option>
    </select>
    <v-select v-model="inputData"
              :options="selectOptions"
              :reduce="data => data.value"
              label="text"
              v-else/>
  </div>
</template>

<script>
import vSelect from "vue-select";

export default {
  name: "FormSelector",
  components: {vSelect},
  props: {
    uuid: String,
    label: String,
    name: String,
    column: {
      default: 12,
      type: Number
    },
    validation: {
      default: () => { return {}},
      type: Object
    },
    value: {
      type: [String, Number, Array]
    },
    selectOptions: Array,
    isArray: {
      default: false,
      type: Boolean
    },
    searchable: {
      default: false,
      type: Boolean
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
    },
    inputData: {
      get() { return this.value },
      set(d) { this.$emit('input', d) }
    },
    isVanilla() {
      return !this.isArray && !this.searchable
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