<template>
  <v-btn v-bind="$attrs" v-on="$listeners" :outlined="outlined" :block="block">
    <slot />
  </v-btn>
</template>
<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  name: 'BaseBtn',
  props: {
    outlined: {
      type: Boolean,
      default: true
    },
    block: {
      type: Boolean,
      default: false
    }
  }
})
</script>
