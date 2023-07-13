<template>
  <v-app class="app bg-grey-lighten-3">
    <v-app-bar app color="primary" dark flat>
      <v-toolbar-title class="text-no-wrap font-weight-bold title">C B</v-toolbar-title>
      <v-spacer></v-spacer>
      <!-- Desktop Menu -->
      <template v-if="!isMediumScreen">
        <v-toolbar-items>
          <div class="d-flex align-center pr-3 nav">
            <v-btn
              v-show="showScrollToTopButton"
              id="up-btn"
              icon="mdi-arrow-up"
              @click="scrollToTop" />
            <v-btn
              density="compact"
              v-for="navItem in navItems"
              :key="navItem.title"
              text
              class="text-subtitle-1"
              @click="scrollToSection(navItem.id)"
            >
              {{ navItem.title }}
            </v-btn>
          </div>
        </v-toolbar-items>
      </template>
      <!-- Mobile Menu -->
      <template v-else>
        <v-btn v-on:click="isMediumScreenMenu = !isMediumScreenMenu" text>
          <v-icon>mdi-menu</v-icon>
        </v-btn>
      </template>
    </v-app-bar>
    <v-navigation-drawer v-model="isMediumScreenMenu" temporary>
      <v-list>
        <v-list-item v-for="navItem in navItems" :key="navItem.title" link @click="scrollToSection(navItem.id)">
          <v-list-item-title>{{ navItem.title }}</v-list-item-title>
        </v-list-item>
        <v-list-item v-show="showScrollToTopButton" link @click="scrollToSection('hero')">
          <v-list-item-title>Return to top</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-main class="main-content">
      <v-container fluid class="ma-0 pa-0">
        <v-row class="bg-grey-lighten-3" justify="center">
          <v-col cols="12" class="pb-0">
            <div class="hero-section">
              <span style="position: relative;">
                <span id="hero" style="position: absolute; top: -50px; left: 0" />
              </span>
              <hero :isMediumScreen="isMediumScreen" :isMobile="isMobile" />
            </div>
          </v-col>
          <v-col cols="12">
            <span style="position: relative;">
              <span id="projects" style="position: absolute; top: -50px; left: 0" />
            </span>
            <projects :isMobile="isMediumScreen" />
          </v-col>
          <v-col cols="12">
            <span style="position: relative;">
              <span id="cool-stuff" style="position: absolute; top: -50px; left: 0" />
            </span>
            <cool-stuff :isMobile="isMediumScreen" />
          </v-col>
          <v-col cols="12">
            <span style="position: relative;">
              <span id="about-me" style="position: absolute; top: -50px; left: 0" />
            </span>
            <about-me :isMobile="isMobile" />
            <!-- Contact Me section content -->
          </v-col>
        </v-row>
      </v-container>
    </v-main>

  <v-footer class="d-flex flex-column w-100 pa-0 bg-grey-lighten-3 footer">
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1440 320">
        <path fill="#160067" fill-opacity="1" d="M0,160L48,138.7C96,117,192,75,288,80C384,85,480,139,576,186.7C672,235,768,277,864,282.7C960,288,1056,256,1152,234.7C1248,213,1344,203,1392,197.3L1440,192L1440,320L1392,320C1344,320,1248,320,1152,320C1056,320,960,320,864,320C768,320,672,320,576,320C480,320,384,320,288,320C192,320,96,320,48,320L0,320Z"></path>
      </svg>
      <div class="footer-details pl-5 pb-2">
        <span class="text-white">&copy; {{ new Date().getFullYear() }} Craig Bennett || Made with VueJs</span>
        <span class="pl-2">
          <v-btn 
            flat 
            icon="mdi-linkedin" 
            variant="text"
            density="compact"
            color="white"  
            href="https://www.linkedin.com/in/craig-bennett-465aa21b4" />
          <v-btn 
            flat
            density="compact"
            variant="text" 
            icon="mdi-github"
            color="white" 
            href="https://github.com/cb91-dev"/>
        </span>
      </div>
    </v-footer>
  </v-app>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';
import AboutMe from './components/AboutMe.vue';
import Hero from './components/Hero.vue';
import Projects from './components/Projects.vue';
import CoolStuff from './components/CoolStuff.vue';

const navItems = ref([
  { title: 'Projects', id: 'projects' },
  { title: 'Cool Stuff', id: 'cool-stuff' },
  { title: 'About Me', id: 'about-me' },
]);

const isMediumScreen = ref(false);
const isMobile = ref(false);
const isMediumScreenMenu = ref(false);
const showScrollToTopButton = ref(false);

const handleResize = () => {
  const screenWidth = window.innerWidth;
  isMobile.value = screenWidth < 450;
  isMediumScreen.value = screenWidth < 768;
};

const handleScroll = () => {
  const heroSection = document.getElementById('hero');
  if (heroSection) {
    const { top } = heroSection.getBoundingClientRect();
    showScrollToTopButton.value = top < -100; // Adjust the threshold as needed
  }
};

const scrollToSection = (sectionId) => {
  const element = document.getElementById(sectionId);
  if (element) {
    element.scrollIntoView({ behavior: 'smooth', block: 'start' });
    isMediumScreenMenu.value = false; // Close the mobile menu after clicking a section
  }
};

const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' });
};

onMounted(() => {
  handleResize();
  window.addEventListener('resize', handleResize);
  window.addEventListener('scroll', handleScroll);
});

onBeforeUnmount(() => {
  window.removeEventListener('resize', handleResize);
  window.removeEventListener('scroll', handleScroll);
});
</script>

<style>
body {
  margin: 0;
  padding: 0;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  overflow: hidden;
  box-sizing: border-box;
}

.app {
  display: flex;
}
.up-btn {
  border-radius: 50%;
}
.footer {
  z-index: 1;
  margin-top: auto;
}

.title {
  width: 150px !important;
}

.footer-details {
  width: 100%;
  background-color: #160067;
}

.footer-icon {
  background-color: none !important;
}

.v-chip-group .v-chip--variant-elevated {
  background-color: #eeeeee !important;
  color: #757575;
}
.footer {
  z-index: 1;
  margin-top: auto;
}

.footer-details {
  width: 100%;
  background-color: #160067;
}
#up-btn {
  width: 22px;
}
</style>
