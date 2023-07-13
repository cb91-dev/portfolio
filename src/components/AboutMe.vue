<template>
  <v-container>
    <v-row align="center" justify="center">
      <v-col cols="12">
        <h3 class="text-center about-me-header">About Me</h3>
        <p class="text-body-2 text-center pt-2">
          Happy you made it down this far so heres my story, My name is Craig Bennett and I am a motivated self-starter web dev based in Brisbane, Queensland. 
        </p>
        <br>
        <p class="text-body-2 text-center">
          When the pandemic started in 2020, I started to evaluate what was important in life and like many I pivoted from a career and industry I was involved in for over 15 years. Leaving behind the automotive coatings and sales industries while challenging, has proven my ability to tackle complex problems, manage time effectively and communicate successfully.
        </p>
        <br>
        <p class="text-body-2 text-center">
          I have always had a keen interest in technology, how things work and how to improve them. This lead me to commence my studies by enrolling in a Diploma of Website Development, which I have successfully graduated from in 2021. Although new to the ICT industry I have a strong belief that with commitment comes success, I am committed to improving my skills and making use of available tools to become a better developer everyday.
        </p>
        <br>
        <p class="text-body-2">
          What more can I say really, I have been bitten by the coding bug and I am loving it!!
        </p>
      </v-col>
    </v-row>
    <v-row align="center" justify="center" class="pt-3">
      <h3 class="text-center about-me-header">Core strengths</h3>
      <v-col cols="12" class="pt-3">
        <div
        :class="{
          'tech-logos-mobile': props.isMobile,
          'tech-logos': !props.isMobile
          }" 
        class="d-flex align-content-center justify-space-evenly">
          <img src='/html5.svg'>
          <img src='/css3.svg'>
          <img src='/javascript.svg'>
          <img src='/nodejs.svg'>
          <img src='/vuejs.svg'>
          <img src='/python.svg'>
          <img src='/react.svg'>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
const props = defineProps({
  isMobile: Boolean,
});

</script>

<style>
.tech-logos {
  height: 55px;
}
.tech-logos-mobile {
  height: 45px;
}
.about-me-header {
display: block;
position: relative; 
}
.about-me-header::after {
content: "";
position: absolute;
bottom: 2px;
width: 120px;
height: 14px;
transform: skew(-12deg) translateX(-95%);
background: rgba(22,0,103,0.1);
}

.about-me-card {
border: 1px solid black;
}

.about-me-card:hover {
border: 2px solid black;
cursor: pointer;
transform: translate(3px, -3px);
}

</style>