<template>
  <v-card-title v-bind="$attrs" v-on="$listeners">
    <slot />
  </v-card-title>
</template>
<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  name: 'BaseCardTitle'
})
</script>
