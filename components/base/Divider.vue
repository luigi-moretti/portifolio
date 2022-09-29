<template>
  <v-divider v-bind="$attrs" v-on="$listeners">
    <slot />
  </v-divider>
</template>
<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  name: 'BaseDivider'
})
</script>
