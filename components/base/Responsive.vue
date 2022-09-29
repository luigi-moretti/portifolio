<template>
  <v-responsive v-bind="$attrs" v-on="$listeners">
    <slot />
  </v-responsive>
</template>
<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  name: 'BaseResponsive'
})
</script>
