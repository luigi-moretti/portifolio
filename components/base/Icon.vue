<template>
  <v-icon v-bind="$attrs" v-on="$listeners">
    <slot />
  </v-icon>
</template>
<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  name: 'BaseIcon'
})
</script>
