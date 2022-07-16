<template>
  <div ref="modal"
       class="modal"
       tabindex="-1">
    <div :class='modalDialogClass'>
      <div class="modal-content" style="min-height: 30rem">

        <div class="modal-header">
          <slot name="header">
            <p class="modal-title mb-0" v-text="header"></p>
            <button
              type='button'
              class='btn-close'
              data-bs-dismiss='modal'
              aria-label='Close'></button>
          </slot>
        </div>

        <div class="modal-body">
          <slot>

          </slot>
        </div>

        <div class="modal-footer">
          <slot name="footer">
            <div class="d-flex flex-wrap-reverse">
              <button
                type='button'
                class='btn btn-link ripple ripple-dark'
                data-bs-dismiss='modal'>
                Cancelar
              </button>
            </div>
          </slot>
        </div>

      </div>
    </div>
  </div>
</template>

<script>
import { Modal } from 'bootstrap'

export default {
  name: "ModalView",
  props: {
    size: {
      type: String,
      default: 'lg'
    },
    header: {
      type: String,
      default: 'Modal'
    },
    modalDialogAlign: {
      type: String,
      default: 'centered'
    },
    value: {
      type: Boolean,
      default: null
    }
  },
  computed: {
    show: {
      get() {
        return this.value === null ? this.modalShow : this.value;
      },
      set(x) {
        this.modalShow = x;
        this.$emit('input', x);
      }
    },
    modalDialogClass() {
      return [
        'modal-dialog',
        'modal-dialog-'+this.modalDialogAlign,
        'modal-dialog-scrollable',
        'modal-'+this.size
      ]
    }
  },
  data() {
    return {
      modalShow: false,
      modal: null
    }
  },
  watch: {
    show(val) {
      if (val) {
        this.modal.show()
      } else {
        this.modal.hide()
      }
    }
  },
  mounted() {
    this.modal = new Modal(this.$refs.modal)
    this.onHide()
  },
  beforeDestroy() {
    this.modal.hide()
  },
  methods: {
    onHide() {
      this.$refs.modal.addEventListener('hide.bs.modal', () => {
        this.show = false
      })
    },
  }
}
</script>

<style scoped>

</style>
