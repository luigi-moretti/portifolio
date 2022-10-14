<template>
  <base-row justify="center">
    <base-col cols="12" sm="8" md="10">
      <home-header :social-medias="socialMedias" :config-home-page="configHomePage" :image-home-page="imageHeader" />
      <base-row>
        <base-col>
          <base-divider />
          <h2 class="text-h4">
            <strong>Trabalhos</strong>
          </h2>
          <base-row dense>
            <base-col v-for="project in projects" :key="project.id" cols="12" md="4" sm="6" xs="12">
              <v-card>
                <v-img :src="project.headerImage.url" class="white--text align-end"
                  gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)" height="200px">
                  <v-card-title v-text="project.title" />
                </v-img>
              </v-card>
            </base-col>
          </base-row>
        </base-col>
      </base-row>
    </base-col>
  </base-row>
</template>

<script lang="ts">
import Vue from 'vue'
import { gql } from 'nuxt-graphql-request'
import HomeHeader from '@/components/modules/home/Header.vue'
import { ISocialMedia } from '~/models/socialMedia'
import { IConfigHomePage } from '~/models/configHomePage'
export default Vue.extend({
  name: 'IndexPage',
  components: {
    HomeHeader
  },
  data: () => ({
    socialMedias: [] as ISocialMedia[],
    configHomePage: {} as IConfigHomePage,
    imageHeader: '',
    projects: []
  }),
  created () {
    this.getSocialMedia()
    this.getConfigHomePage()
    this.getProjects()
  },
  methods: {
    async getSocialMedia () : Promise<void> {
      const query = gql`
      query SocialMedia {
          allSocials {
            label
            link
            nameIcon
          }
        }
      `
      const { allSocials } = await this.$graphql.default.request(query)
      this.socialMedias = allSocials
    },
    async getConfigHomePage () : Promise<void> {
      const query = gql`
      query ConfigHomePage {
        configSite {
            title
            headerImage {
              url
              height
              width
            }
          }
        }
      `
      const { configSite } = await this.$graphql.default.request(query)
      this.configHomePage = configSite
      this.imageHeader = configSite.headerImage.url
    },
    async getProjects () : Promise<void> {
      const query = gql`
      query Projects {
        allProjects {
          title
          id
          headerImage {
            url
            alt
          }
        }
      }
      `
      const { allProjects } = await this.$graphql.default.request(query)
      this.projects = allProjects
    }
  }
})
</script>
