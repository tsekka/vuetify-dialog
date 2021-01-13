<template>
  <!--
    USAGE EXAMPLE:
    async cancelSubscription(){
            let response = await this.$dialog.confirm({
            title: "Teenuse lõpetamine",
            text: 'Kas oled kindel, et soovid teenuse lõpetada?',
            actions: {
                false: "Ei, muutsin meelt",
                true: {
                    text: "Jah",
                    color: "primary",
                },
            },
        });
        if (response) {
            this.cancelSubscription();
        }
    }
 -->
  <v-card>
    <v-toolbar v-if="Boolean(type)" dark :color="getColor" dense flat>
      <v-icon v-if="Boolean(getIcon)" left>{{ getIcon }}</v-icon>
      <v-toolbar-title v-text="title"></v-toolbar-title>
    </v-toolbar>
    <v-card-title v-if="!type">
      <h3 class v-text="title" />
    </v-card-title>
    <v-card-text class="text-body-1 py-2" v-html="text" />
    <v-card-actions>
      <v-spacer />
      <DialogActions :actions="actions" flat />
    </v-card-actions>
  </v-card>
</template>

<script>
import Confirmable from "vuedl/src/mixins/confirmable";
import Colorable from "../mixins/colorable";
import DialogActions from "./DialogActions.vue";
import {
  VCard,
  VCardTitle,
  VCardText,
  VCardActions,
  VToolbar,
  VToolbarTitle,
  VIcon,
  VSpacer,
} from "vuetify/lib";

export default {
  components: {
    DialogActions,
    VCard,
    VCardTitle,
    VCardText,
    VCardActions,
    VToolbar,
    VToolbarTitle,
    VIcon,
    VSpacer,
  },
  layout: ["default", { width: 450 }],
  mixins: [Confirmable, Colorable],
  props: {
    icon: {
      type: [String, Boolean],
      default: undefined,
    },
    text: {
      type: [String, Function],
      required: true,
      default: "",
    },
    test: {
      default: "test",
    },
  },
  computed: {
    getIcon() {
      if (this.icon === false) return;
      if (this.icon) return this.icon;
      if (
        this.$vuetify &&
        this.$vuetify.icons &&
        this.$vuetify.icons.values &&
        this.$vuetify.icons.values[this.type]
      ) {
        return this.$vuetify.icons.values[this.type];
      }
      return null;
    },
    getText() {
      return typeof this.text === "function" ? this.text() : this.text;
    },
  },
};
</script>
