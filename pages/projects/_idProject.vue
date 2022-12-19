<template>
  <div>
    <h1>Projeto: {{ project.title }}</h1>
    <div v-if="loading">
      Loading...
    </div>
    <div v-else-if="error">
      Something bad happened!
    </div>
    <div v-else>
      <datocms-structured-text
        :data="projectBody.value"
        :render-block="renderBlock"
      />
      <!-- {{ projectBody.value.schema }} -->
    </div>
  </div>
</template>
<script lang="ts">
import Vue from 'vue'
import { gql } from 'nuxt-graphql-request'
import { StructuredText, Image } from 'vue-datocms'

export default Vue.extend({
  name: 'ProjectPage',
  components: {
    // eslint-disable-next-line vue/no-unused-components
    'datocms-structured-text': StructuredText,
    // eslint-disable-next-line vue/no-unused-components
    'datocms-image': Image
  },
  data () {
    return {
      idProject: '' as any,
      project: '' as any,
      projectBody: {} as any,
      loading: false,
      error: false
    }
  },
  created () {
    this.idProject = this.$route.query.idProject
  },
  async mounted () {
    await this.getProject(this.idProject)
  },
  methods: {
    async getProject (idProject:string):Promise<void> {
      this.loading = true
      const query = gql`
      query GetProject {
        project(filter: {id: {eq: "${idProject}"}}) {
          id
          title
          body {
            value
            blocks {
              __typename
              ... on SimpleImageRecord {
                id
                image {
                  responsiveImage {
                    src
                    srcSet
                    sizes
                    height
                    base64
                  }
                }
              }
            }
            links {
              id
              title
            }
          }
        }
      }
      `
      const { project } = await this.$graphql.default.request(query)
      this.project = project
      this.projectBody = project.body
      console.log(this.projectBody.value.schema)
      this.loading = false
    },
    renderInlineRecord: ({ record, h }:{ record:any, h:any }) => {
      console.log('renderInlineRecord', { record, h })
      if (record.__typename === 'BlogPostRecord') {
        return h('a', { href: `/blog/${record.slug}` }, [record.title])
      }
      return null
    },
    renderLinkToRecord: ({ record, h, children }:{ record:any, h:any, children:any }) => {
      console.log('renderLinkToRecord', { record, h, children })

      if (record.__typename === 'BlogPostRecord') {
        return h('a', { href: `/blog/${record.slug}` }, children)
      }
      return null
    },
    renderBlock: ({ record, key, h }: {record:any, key:any, h:any}) => {
      console.log('renderBlock', { record, key, h })

      if (record.__typename === 'ImageBlockRecord') {
        return h('datocms-image', { key, props: { data: record.image.responsiveImage } })
      }

      if (record.__typename === 'SimpleImageRecord') {
        return h('datocms-image', { key, props: { data: record.image.responsiveImage } })
      }
      return null
    }
  }
})
</script>
