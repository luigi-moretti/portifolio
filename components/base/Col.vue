<template>
  <v-col v-bind="$attrs" v-on="$listeners">
    <slot />
  </v-col>
</template>
<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  name: 'BaseCol'
})
</script>
