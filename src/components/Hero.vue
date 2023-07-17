<template>
  <div :class="{
    'hero-container': !props.isMediumScreen,
    'hero-container-medium ': props.isMediumScreen,
    'hero-container-mobile': props.isMobile,
    }"
    class="d-flex justify-space-evenly align-center"
    >
      <v-card
        flat
        color="#160067"
        class="text-white overflow-show"
        max-width="344"
      >
        <v-card-text class="pl-1 ">
          <h2 class="title-text-first">Hello I am</h2>
          <p :class="{
            'text-h4 text--primary title-text-second': !props.isMobile,
            'text-h5 text--primary title-text-second': props.isMobile }">
          Craig Bennett
          </p>
          <div class="text--primary pt-1 pb-1">
          Full Stack Developer<br>
          <div class="d-flex">
            <v-chip-group>
              <v-chip prepend-icon="mdi-linkedin" href="https://www.linkedin.com/in/craig-bennett-465aa21b4">Linkedin</v-chip>

              <v-chip prepend-icon="mdi-github" href="https://github.com/cb91-dev">Git Hub</v-chip>
            </v-chip-group>
          </div>
        </div>
        </v-card-text>
        <v-card-actions class="pt-0">
        <v-btn
        prepend-icon="mdi-download"
        variant="outlined"
        text
        href="/Resume.pdf"
        >
        Download CV
        </v-btn>
        </v-card-actions>
      </v-card>
    <div>
      <img :class="
        {'hero-image-container': !props.isMediumScreen, 
        'hero-image-container-medium': props.isMediumScreen,
        'hero-image-container-mobile': props.isMediumScreen && props.isMobile,
        }" 
        src="/head_shot.png">
    </div>
    </div>
    <svg class="wave-shape" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1440 320">
      <path fill="#160067"  fill-opacity="1" d="M0,64L48,90.7C96,117,192,171,288,202.7C384,235,480,245,576,213.3C672,181,768,107,864,80C960,53,1056,75,1152,69.3C1248,64,1344,32,1392,16L1440,0L1440,0L1392,0C1344,0,1248,0,1152,0C1056,0,960,0,864,0C768,0,672,0,576,0C480,0,384,0,288,0C192,0,96,0,48,0L0,0Z">
      </path>
    </svg>
</template>


<script setup>

const props = defineProps({
  isMediumScreen: Boolean,
  isMobile: Boolean,
});

</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Oswald:wght@300;400;500&display=swap');

.title-text-first { 
  font-family: 'Oswald', sans-serif;
  font-weight: 300;
  font-size: 38px;
  padding-bottom: 20px;
  z-index: 99999;
}
.title-text-second { 
  font-family: 'Oswald', sans-serif;
  font-weight: 400;
}
.overflow-show {
  overflow: visible !important;
}
.hero-container {
  padding-top: 180px;
  height: 320px;
  background-color: #160067;
  z-index: 2;
}
.hero-container-medium {
  padding-top: 20px;
  height: 220px;
  background-color: #160067;
  z-index: 2;
}
.hero-container-mobile {
  padding-top: 20px;
  height: 220px;
  background-color: #160067;
  z-index: 2;
}
.hero-image-container {
  height: 260px;
  position: relative;
  z-index: 2;
}
.hero-image-container-medium {
  height: 160px;
  position: relative;
  z-index: 2;
}
.hero-image-container-mobile {
  height: 100px;
  position: relative;
  z-index: 2;
}
.wave-shape {
  z-index: -10;
}

</style>