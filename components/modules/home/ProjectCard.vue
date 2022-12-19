<template>
  <base-card
    v-ripple
    class="cursor-pointer"
    @click="goToProject(project)"
  >
    <base-img
      :src="project.headerImage.url"
      class="white--text align-end"
      gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
      height="200px"
    >
      <base-card-title v-text="project.title" />
    </base-img>
  </base-card>
</template>
<script lang="ts">
import Vue, { PropType } from 'vue'
import { IProject } from '~/models/project'
export default Vue.extend({
  name: 'HomeProjectCard',
  props: {
    project: {
      type: Object as PropType<IProject>,
      required: true
    }
  },
  methods: {
    goToProject (project: IProject) {
      this.$router.push({
        path: '/projects',
        query: { idProject: project.id }
      })
    }
  }
})
</script>
