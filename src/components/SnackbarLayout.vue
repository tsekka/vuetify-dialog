<style lang="scss">
.toast .v-alert {
  width: 100%;
  .v-alert__icon {
    box-shadow: 0 2px 1px -1px rgba(0, 0, 0, 0.2), 0 1px 1px 0 rgba(0, 0, 0, 0.14),
      0 1px 3px 0 rgba(0, 0, 0, 0.12) !important;
  }
}
</style>
<template>
  <v-snackbar
    :timeout="timeout || 1000000"
    v-model="isActive"
    :top="top"
    :left="left"
    :right="right"
    :bottom="bottom"
    @click="dismiss"
    :dismissible="false"
  >
    <div class="d-flex align-center justify-space-between">
      <dialog-child v-bind="$options.propsData" ref="dialog" />
      <v-btn small color="pink" icon @click="isActive = false">
        <v-icon>mdi-close</v-icon>
      </v-btn>
    </div>
  </v-snackbar>
</template>

<script>
// import Colorable from "../mixins/colorable";
// import { VSnackbar } from "vuetify/lib";

export default {
  //   components: {
  //     VSnackbar,
  //   },
  //   mixins: [Colorable],
  props: {
    timeout: Number,
    position: String,
  },
  data() {
    const position = this.position || this.$options.propsData.position || "";
    return {
      top: position.indexOf("top") !== -1,
      left: position.indexOf("left") !== -1,
      right: position.indexOf("right") !== -1,
      bottom: position.indexOf("bottom") !== -1,
    };
  },
  methods: {
    _destroy() {
      setTimeout(() => {
        this.$destroy();
      }, 500);
    },
  },
};
</script>
