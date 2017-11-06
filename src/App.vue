<template lang="html">
  <div class="w3-container">

    <div class="w3-container w3-leftbar w3-border-blue w3-center w3-pale-blue" style="margin-top: 10px;">
      <h1>Vuejs Tabs</h1>
    </div>

    <div class="w3-container w3-border w3-light-grey" style="margin-top: 20px;">
      <p>This Tabs App was built with Vuejs and uses dynamic components and Velocity.js for the transitions.</p>
    </div>


    <div class="w3-bar w3-center" style="margin: 20px 0;">
      <button
      class="w3-button w3-blue w3-round"
      @click="selectedComponent = 'appFirstTab'"
      >Latin</button>

      <button
      class="w3-button w3-orange w3-round"
      @click="selectedComponent = 'appSecondTab'"
      >Italian</button>

      <button
      class="w3-button w3-green w3-round"
      @click="selectedComponent = 'appThirdTab'"
      >French</button>
    </div>

    <transition
    @before-enter="beforeEnter"
    @enter = "enter"
    @leave = "leave"
    :css="false">

      <component
      class="component"
      :is="selectedComponent"
      ></component>

    </transition>

  </div>
</template>

<script>
import FirstTab from './components/FirstTab.vue';
import SecondTab from './components/SecondTab.vue';
import ThirdTab from './components/ThirdTab.vue';

export default {
  data() {
    return {
      selectedComponent: 'appFirstTab'
    }
  },

  components: {
    appFirstTab: FirstTab,
    appSecondTab: SecondTab,
    appThirdTab: ThirdTab
  },

  methods: {
    beforeEnter(selectedComponent) {
      selectedComponent.style.opacity = 0
    },
    enter(selectedComponent, done) {
      Velocity(selectedComponent, 'transition.fadeIn', {delay: 2000, duration: 1000}, {stagger: 250}, {complete: done})
    },
    leave(selectedComponent, done) {
      Velocity(selectedComponent, 'transition.slideLeftOut', {duration: 2000}, {complete: done})
    }
  }
}
</script>

<style lang="css">
  .component {
    position: absolute;
    border-left: 2px solid lightgrey;
    margin-right: 15px;
    margin-bottom: 50px;
  }
</style>
