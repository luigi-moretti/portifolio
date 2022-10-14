<template>
  <v-fab-transition v-bind="$attrs" v-on="$listeners">
    <slot />
  </v-fab-transition>
</template>
<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  name: 'BaseFabTransition'
})
</script>
