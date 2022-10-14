<template>
  <base-row justify="center">
    <base-col ref="homeapp" cols="12" sm="8" md="10">
      <home-header
        :social-medias="socialMedias"
        :config-home-page="configHomePage"
        :image-home-page="imageHeader"
        @goTo="goTo"
      />
      <base-row>
        <base-col>
          <base-divider />
          <h2 ref="projects" class="text-h4 my-3">
            <strong>Projetos</strong>
          </h2>
          <base-row dense>
            <base-col
              v-for="project in projects"
              :key="project.id"
              cols="12"
              md="4"
              sm="6"
              xs="12"
            >
              <base-card>
                <base-img
                  :src="project.headerImage.url"
                  class="white--text align-end"
                  gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
                  height="200px"
                >
                  <base-card-title v-text="project.title" />
                </base-img>
              </base-card>
            </base-col>
          </base-row>
        </base-col>
      </base-row>
      <base-fab-transition>
        <base-btn
          :outlined="false"
          v-scroll="onScroll"
          v-show="config.showFabButton"
          @click="goTop"
          color="primary"
          fixed
          fab
          bottom
          right
        >
          <v-icon>mdi-chevron-up</v-icon>
        </base-btn>
      </base-fab-transition>
    </base-col>
  </base-row>
</template>

<script lang="ts">
import Vue from 'vue'
import { gql } from 'nuxt-graphql-request'
import HomeHeader from '@/components/modules/home/Header.vue'
import { ISocialMedia } from '~/models/socialMedia'
import { IConfigHomePage } from '~/models/configHomePage'
import { IProject } from '~/models/project'
export default Vue.extend({
  name: 'IndexPage',
  components: {
    HomeHeader
  },
  data: () => ({
    socialMedias: [] as ISocialMedia[],
    configHomePage: {} as IConfigHomePage,
    imageHeader: '',
    projects: [] as IProject[],
    config: {
      showFabButton: false
    }
  }),
  created () {
    this.getSocialMedia()
    this.getConfigHomePage()
    this.getProjects()
  },
  methods: {
    onScroll (e: any): void {
      if (typeof window === 'undefined') { return }
      const top = window.pageYOffset || e.target.scrollTop || 0
      this.config.showFabButton = top > 50
    },
    goTo (refName:string) {
      const element = this.$refs[refName]
      if (element) {
        const top = element.offsetTop
        window.scrollTo({
          top,
          behavior: 'smooth'
        })
      }
    },
    goTop () {
      window.scrollTo({
        top: 0,
        behavior: 'smooth'
      })
    },
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
