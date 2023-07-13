<template>
  <v-container>
    <v-row align="center" justify="center">
      <v-col cols="8">
        <h3 class="text-center cool-stuff-header">Cool Stuff</h3>
        <p class="text-center pt-2 text-body-2">I am always playing around with something cool take a look for youself.</p>
      </v-col>
    </v-row>
    <v-row justify="start" align-content="center">
      <v-col
        v-for="(item, index) in coolStuffInfo"
        :key="`cool-stuff-${index}`"
        :cols="props.isMobile ? 12 : 6"
        class="my-2"
      >
        <v-card
          class=" cool-stuff-card"
          height="175"
          @mouseenter="startAnimation" 
          @mouseleave="stopAnimation"
        >
          <div class="cog-container">
            <div class="cog"></div>
          </div>
          <v-card-text>
            <h5>{{ item.title }}</h5>
            <div class="text-caption">
              {{  item.description }}
            </div>
          </v-card-text>
          <v-card-actions class="pt-0 ml-2 d-flex flex-column justify-content-center align-start">
            <v-chip-group>
              <v-chip
                v-for="skill, i in item.skills"
                :key="`skills-${i}`" 
                class="text-caption"
                density="compact"
                :prepend-icon="skill.icon" 
                variant="elevated"
              >
              {{ skill.name }}
              </v-chip>
            </v-chip-group>
            <div class="cool-stuff-links pt-2">
              <v-btn
                v-if="item.gitHubLink"
                prepend-icon="mdi-github"
                density="compact"
                variant="outlined"
                class="text-body-2"
                :href="item.gitHubLink" 
                >
                Git Hub
              </v-btn>
              <v-btn 
                v-if="item.liveLink"
                color="primary"
                class="text-body-2"
                density="compact"
                variant="outlined"
                :href="item.liveLink" 
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

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';

const props = defineProps({
  isMobile: Boolean,
});
const extraCard = ref(null);
const spinning = ref(null);

const coolStuffInfo = 
  [
    {
      title: 'Products Api',
      description: 'A typescript product API, built using AWS and framework Serverless.',
      skills: [{ name:'TypeScript', icon: 'mdi-language-typescript'},{ name: 'AWS', icon: 'mdi-aws'},{name: 'Serverless', icon: 'mdi-server' }],
      gitHubLink: 'https://github.com/cb91-dev/products-api',
    },
    {
      title: 'Kounter',
      description: 'A Python GUI app built to take in csv type files and return total counts of all and per file.',
      skills: [{ name: 'Python', icon: 'mdi-language-python' }],
      gitHubLink: 'https://github.com/cb91-dev/kounter',
    },
    {
      title: 'Alan News',
      description: 'Quick app that uses Alan AI to read the news for you give it a go.',
      skills: [
        { name: 'Javascript', icon: 'mdi-language-javascript'}, 
        { name: 'Alan AI', icon: 'mdi-data-matrix'},
        {name: 'ReactJs', icon: 'mdi-react'}],
      gitHubLink: 'https://github.com/cb91-dev/kounter',
      liveLink: 'https://master.dpti1owqc79yo.amplifyapp.com'
    },
    {
      title: 'Fake Pypi',
      description: 'A serverside Python app, I am just trying to copy https://pypi.org/.',
      skills: [{ name: 'Python', icon: 'mdi-language-python' }],
      gitHubLink: 'https://github.com/cb91-dev/Fake_Pypi',
    },
    {
      title: 'Pong Championship',
      description: 'A classic remake of pong, using Python and Pygame',
      skills: [{ name: 'Python', icon: 'mdi-language-python' }],
      gitHubLink: 'https://github.com/cb91-dev/pong',
    }
  ];

const startAnimation = () => {
  spinning.value = true; 
}
const stopAnimation = () => {
  spinning.value = false; 
}

</script>

<style>
.cool-stuff-header {
 display: block;
 position: relative; 
}  
.cool-stuff-header::after {
  content: "";
  position: absolute;
  bottom: 2px;
  width: 120px;
  height: 14px;
  transform: skew(-12deg) translateX(-95%);
  background: rgba(22,0,103,0.1);
}
.cog-container {
  position: absolute;
  bottom: -20px;
  right: -30px;
  width: 100%;
  height: 100%;
  display: flex;
  overflow: hidden;
  align-items: end;
  justify-content: end;
  pointer-events: none;
}

.cog {
  width: 100px;
  height: 100px;
  background-image: url('/cog.png');
  background-repeat: no-repeat;
  background-size: cover;
  opacity: 0.5;
  transition: transform 0.5s;
}

.cool-stuff-card:hover .cog {
  animation: spinCog 4s infinite linear;
}

@keyframes spinCog {
  from {
    transform: rotate(0);
  }
  to {
    transform: rotate(360deg);
  }
}
.cool-stuff-card {
  border: 1px solid #160067;
  position: relative;
}

.cool-stuff-card:hover {
  border: 2px solid #160067;
  cursor: pointer;
}
.cool-stuff-links .v-btn:hover {
  background-color: rgba(22,0,103,0.3) !important;
}

</style>