<template>
  <v-row v-bind="$attrs" v-on="$listeners">
    <slot />
  </v-row>
</template>
<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  name: 'BaseRow'
})
</script>
