<template>
  <base-row justify="center">
    <base-col cols="12" sm="8" md="10">
      <div>
        <base-responsive :aspect-ratio="16/9">
          <base-row class="mt-5">
            <base-col>
              <h1 class="text-h2">
                <strong>Olá,</strong><br>
                <span>Eu me chamo <strong>Luigi!</strong>
                  <span>{{ title.typeValue }}</span>
                  <span class="blinking-cursor-title">|</span>
                  <span class="cursor" :class="{ typing: title.typeStatus }">&nbsp;</span>
                </span>
              </h1>
              <p class="text-subtitle-1 mt-3">
                Sou desenvolvedor
                <span>{{ subtitle.typeValue }}</span>
                <span class="blinking-cursor">|</span>
                <span class="cursor" :class="{ typing: subtitle.typeStatus }">&nbsp;</span>
              </p>
              <p class="text-subtitle-1 mt-3">
                Gosto de resolver problemas e criar soluções que impactam.
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
    ],
    title: {
      typeValue: '',
      typeStatus: false,
      displayTextArray: ['🤓️', '👨‍💻️', '☕️', '🇧🇷️'],
      typingSpeed: 100,
      erasingSpeed: 100,
      newTextDelay: 2000,
      displayTextArrayIndex: 0,
      charIndex: 0
    },
    subtitle: {
      typeValue: '',
      typeStatus: false,
      displayTextArray: ['Front-end Developer', 'UX Designer', 'Freelancer'],
      typingSpeed: 100,
      erasingSpeed: 100,
      newTextDelay: 2000,
      displayTextArrayIndex: 0,
      charIndex: 0
    }
  }),
  created () {
    setTimeout(this.typeTextSubtitle, this.subtitle.newTextDelay + 200)
    setTimeout(this.typeTextTitle, this.title.newTextDelay + 200)
  },
  methods: {
    typeTextSubtitle () {
      if (this.subtitle.charIndex < this.subtitle.displayTextArray[this.subtitle.displayTextArrayIndex].length) {
        if (!this.subtitle.typeStatus) { this.subtitle.typeStatus = true }
        this.subtitle.typeValue += this.subtitle.displayTextArray[this.subtitle.displayTextArrayIndex].charAt(this.subtitle.charIndex)
        this.subtitle.charIndex += 1
        setTimeout(this.typeTextSubtitle, this.subtitle.typingSpeed)
      } else {
        this.subtitle.typeStatus = false
        setTimeout(this.eraseTextSubtitle, this.subtitle.newTextDelay)
      }
    },
    eraseTextSubtitle () {
      if (this.subtitle.charIndex > 0) {
        if (!this.subtitle.typeStatus) { this.subtitle.typeStatus = true }
        this.subtitle.typeValue = this.subtitle.displayTextArray[this.subtitle.displayTextArrayIndex].substring(0, this.subtitle.charIndex - 1)
        this.subtitle.charIndex -= 1
        setTimeout(this.eraseTextSubtitle, this.subtitle.erasingSpeed)
      } else {
        this.subtitle.typeStatus = false
        this.subtitle.displayTextArrayIndex += 1
        if (this.subtitle.displayTextArrayIndex >= this.subtitle.displayTextArray.length) {
          this.subtitle.displayTextArrayIndex = 0
        }
        setTimeout(this.typeTextSubtitle, this.subtitle.typingSpeed + 1000)
      }
    },
    typeTextTitle () {
      if (this.title.charIndex < this.title.displayTextArray[this.title.displayTextArrayIndex].length) {
        if (!this.title.typeStatus) { this.title.typeStatus = true }
        this.title.typeValue = this.title.displayTextArray[this.title.displayTextArrayIndex]
        this.title.charIndex += 1
        setTimeout(this.typeTextTitle, this.title.typingSpeed)
      } else {
        this.title.typeStatus = false
        setTimeout(this.eraseTextTitle, this.title.newTextDelay)
      }
    },
    eraseTextTitle () {
      if (this.title.charIndex > 0) {
        if (!this.title.typeStatus) { this.title.typeStatus = true }
        this.title.typeValue = ''
        this.title.charIndex -= 1
        setTimeout(this.eraseTextTitle, this.title.erasingSpeed)
      } else {
        this.title.typeStatus = false
        this.title.displayTextArrayIndex += 1
        if (this.title.displayTextArrayIndex >= this.title.displayTextArray.length) {
          this.title.displayTextArrayIndex = 0
        }
        setTimeout(this.typeTextTitle, this.title.typingSpeed + 1000)
      }
    }
  }
})
</script>
<style scoped>
.blinking-cursor {
  font-size: 1rem;
  color: #2c3e50;
  -webkit-animation: 1s blink step-end infinite;
  -moz-animation: 1s blink step-end infinite;
  -ms-animation: 1s blink step-end infinite;
  -o-animation: 1s blink step-end infinite;
  animation: 1s blink step-end infinite;
}
.blinking-cursor-title {
  font-size: 3.75rem;
  color: #2c3e50;
  -webkit-animation: 1s blink step-end infinite;
  -moz-animation: 1s blink step-end infinite;
  -ms-animation: 1s blink step-end infinite;
  -o-animation: 1s blink step-end infinite;
  animation: 1s blink step-end infinite;
}
@keyframes blink {
  from,
  to {
    color: transparent;
  }
  50% {
    color: #2c3e50;
  }
}
@-moz-keyframes blink {
  from,
  to {
    color: transparent;
  }
  50% {
    color: #2c3e50;
  }
}
@-webkit-keyframes blink {
  from,
  to {
    color: transparent;
  }
  50% {
    color: #2c3e50;
  }
}
@-ms-keyframes blink {
  from,
  to {
    color: transparent;
  }
  50% {
    color: #2c3e50;
  }
}
@-o-keyframes blink {
  from,
  to {
    color: transparent;
  }
  50% {
    color: #2c3e50;
  }
}
</style>
