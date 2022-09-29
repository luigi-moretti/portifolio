<template>
  <base-row justify="center">
    <base-col cols="12" sm="8" md="10">
      <div>
        <base-responsive :aspect-ratio="16/9">
          <base-row class="mt-5">
            <base-col>
              <h1 class="text-h2">
                <strong>Olá,</strong><br>
                <span>Eu me chamo <strong>Luigi!</strong> :)</span>
              </h1>
              <p class="text-subtitle-1 mt-3">
                Sou desenvolvedor front-end e UX designer. Gosto de resolver
                problemas e criar soluções que impactam.
              </p>
            </base-col>
          </base-row>
          <base-row>
            <base-col cols="12">
              <base-btn icon :outlined="false">
                <base-icon>mdi-github</base-icon>
              </base-btn>
              <base-btn icon :outlined="false">
                <base-icon>mdi-linkedin</base-icon>
              </base-btn>
              <base-btn icon :outlined="false">
                <base-icon>mdi-instagram</base-icon>
              </base-btn>
            </base-col>
          </base-row>
          <base-row class="mb-1">
            <base-col cols="12">
              <base-btn class="mr-2" color="primary">
                <base-icon left>
                  mdi-briefcase
                </base-icon>
                Trabalhos
              </base-btn>
              <base-btn class="mx-2">
                <base-icon left>
                  mdi-information
                </base-icon>
                Sobre mim
              </base-btn>
            </base-col>
          </base-row>
        </base-responsive>
      </div>
      <base-row>
        <base-col>
          <base-divider />
          <h2 class="text-h4">
            <strong>Trabalhos</strong>
          </h2>
          <base-row dense>
            <base-col
            v-for="project in projects"
            :key="project.title"
            cols="12"
            md="4"
            sm="6"
            xs="12">
              <v-card>
                <v-img
                  :src="project.image"
                  class="white--text align-end"
                  gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
                  height="200px">
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
export default Vue.extend({
  name: 'IndexPage',
  data: () => ({
    projects: [
      {
        title: 'Projeto 01',
        image: 'https://cdn.vuetifyjs.com/images/cards/plane.jpg'
      },
      {
        title: 'Projeto 02',
        image: 'https://cdn.vuetifyjs.com/images/cards/plane.jpg'
      },
      {
        title: 'Projeto 03',
        image: 'https://cdn.vuetifyjs.com/images/cards/plane.jpg'
      },
      {
        title: 'Projeto 04',
        image: 'https://cdn.vuetifyjs.com/images/cards/plane.jpg'
      },
      {
        title: 'Projeto 05',
        image: 'https://cdn.vuetifyjs.com/images/cards/plane.jpg'
      },
      {
        title: 'Projeto 06',
        image: 'https://cdn.vuetifyjs.com/images/cards/plane.jpg'
      },
      {
        title: 'Projeto 07',
        image: 'https://cdn.vuetifyjs.com/images/cards/plane.jpg'
      }
    ]
  })
})
</script>
