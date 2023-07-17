<template>
  <v-container>
    <v-row align="center" justify="center" class="pb-0">
      <v-col cols="8" class="pb-0">
        <h3 class="text-center projects-header">Projects</h3>
        <p class="text-center pt-2 text-body-2 mb-0">
          Showcasing completed projects with a focus on innovation and continuous learning.
        </p>
      </v-col>
    </v-row>
    <v-row 
      v-for="project, index in projectsInfo" 
      :key="`project-cards-${index}`" 
      :class="isMobile ? 'flex-column' : 'flex-row'"
      >
      <v-col>
        <Carousel :autoplay="3000" :wrap-around="true">
          <Slide v-for="slide in project.images" :key="slide">
            <div class="carousel-item">
              <img class="carousel-image" :src="slide"/>
            </div>
          </Slide>
        </Carousel>
      </v-col>
      <v-col
      :class="{
      'order-last': project.order === 2 && !isMobile, 
      'order-first': project.order == 1 && !isMobile 
      }">
        <v-card height="218px" variant="flat">
          <v-card-item class="pt-0">
            <v-card-title 
            :class="project.title === 'House' ? 'house-font' : 'notetaker-font'">
              {{ project.title }}
            </v-card-title>
          </v-card-item>
          <v-card-text>
            {{ project.description }}
            <v-chip-group>
              <v-chip
                v-for="skill, i in project.skills"
                :key="`skills-${i}`" 
                class="text-caption projects-chips"
                density="compact"
                :prepend-icon="skill.icon" 
                variant="elevated"
              >
              {{ skill.name }}
              </v-chip>
            </v-chip-group>
          </v-card-text>
          <v-card-actions>
            <div class="projects-links pt-2 pl-2">
              <v-btn
                v-if="project.gitHubLink"
                prepend-icon="mdi-github"
                density="compact"
                variant="outlined"
                class="text-body-2"
                :href="project.gitHubLink" 
                >
                Git Hub
              </v-btn>
              <v-btn 
                v-if="project.liveLink"
                color="primary"
                class="text-body-2"
                density="compact"
                variant="outlined"
                :href="project.liveLink" 
                prepend-icon="mdi-web">
                Live
              </v-btn>
            </div>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
import { defineComponent } from 'vue'
import { Carousel, Slide } from 'vue3-carousel'
import 'vue3-carousel/dist/carousel.css'

export default defineComponent({
  name: 'Autoplay',
  data() {
    return {
      projectsInfo: [
      {
        title: 'House',
        description: 'House is a real estate application, where users can find and search properties for either renting or purchasing.',
        skills: [{ name:'Next.js', icon: 'mdi-alpha-n-circle-outline'},{ name: 'Chakra UI', icon: 'mdi-lightning-bolt'},{name: 'Rapid API', icon: 'mdi-server' }],
        gitHubLink: 'https://github.com/cb91-dev/house',
        liveLink: 'https://house-one.vercel.app/',
        order: 1,
        images: [
          '/house_1.png',
          '/house_2.png',
          '/house_3.png',
        ],
      },
      {
      title: 'Note Taker',
      description: 'NoterTaker the word says it all',
      skills: [
        { name:'Vue.js', icon: 'mdi-vuejs'},
        { name: 'Pinia', icon: 'mdi-fruit-pineapple'},
        {name: 'Tailwind CSS', icon: 'mdi-tailwind' },
        {name: 'FireBase', icon: 'mdi-firebase' },
        {name: 'FireStore', icon: 'mdi-firebase' }],
      liveLink: 'https://notetaker-32363.web.app',
      gitHubLink: 'https://github.com/cb91-dev/NoteTaker',
      order: 2,
        images: [
        '/notetaker_1.png',
        '/notetaker_2.png',
        '/notetaker_3.png',
      ],
    }
      ],
      loading: false,
    }
  },
  props: { isMobile: Boolean},
  components: {
    Carousel,
    Slide,

  },
})

const CarouselComponent = Carousel;
const SlideComponent = Slide;


export { CarouselComponent as Carousel, SlideComponent as Slide };

</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+JP&family=Rubik+Moonrocks&display=swap');

.notetaker-font {
  font-family: 'Rubik Moonrocks', cursive;
  color: rgb(74, 222, 128);
  font-size: 2em;
}
.house-font {
  font-family: 'Noto Sans JP', sans-serif;
  color: rgb(66, 153, 225);
  font-weight: 600;
  font-size: 2em;
}
.projects-chips {
  border: 1px solid #160067;
  padding: 11px;
}
.carousel-item {
  position: relative;
  width: 100%;
  padding-top: 56.25%; /* 16:9 aspect ratio */
}

.carousel-image {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.projects-header {
 display: block;
 position: relative; 
}  
.projects-header::after {
  content: "";
  position: absolute;
  bottom: 2px;
  width: 120px;
  height: 14px;
  transform: skew(-12deg) translateX(-95%);
  background: rgba(22,0,103,0.1);
}
.v-col .v-card--variant-flat {
  background-color: transparent !important;
}
</style>