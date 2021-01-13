<style lang="scss">
.vuedl-notification {
  overflow: visible !important;
  .v-alert__icon {
    margin-right: 10px;
    top: -28px;
    box-shadow: 0 2px 1px -1px rgba(0, 0, 0, 0.2),
      0 1px 1px 0 rgba(0, 0, 0, 0.14), 0 1px 3px 0 rgba(0, 0, 0, 0.12) !important;
  }
}
</style>
<template>
  <base-material-alert
    style="margin: 0; min-width: 300px"
    @input="$emit('submit')"
    :dismissible="dismissible"
    :type="color"
    :outlined="outlined"
    :prominent="prominent"
  >
    <div class="d-flex align-center">
      <div class="mr-2" v-html="text"></div>
      <DialogActions :actions="actions" />
    </div>
  </base-material-alert>
</template>
<script>
import DialogActions from "./DialogActions.vue";
import { VAlert } from "vuetify/lib";

export default {
  components: {
    DialogActions,
    VAlert,
  },
  layout: ["notification", { showClose: false }],
  props: {
    color: {
      type: String,
      default: () => "info",
    },
    actions: {
      type: [Array, Object],
      default: () => {},
    },
    text: {
      type: String,
      default: "",
    },
    outlined: Boolean,
    prominent: Boolean,
    dismissible: {
      type: Boolean,
      default: true,
    },
  },
};
</script>
