<template lang="html">
  <div class="w3-container">

    <div class="w3-container w3-border w3-light-grey" style="margin-top: 20px;">
      <p class="w3-center">Tabs using Vuejs Dynamic Components</p>
    </div>


    <div class="w3-bar w3-center" style="margin: 20px 0;">
      <button
      class="w3-button w3-blue w3-round"
      @click="selectedComponent = 'appFirstTab'"
      >Lorem</button>

      <button
      class="w3-button w3-orange w3-round"
      @click="selectedComponent = 'appSecondTab'"
      >Ipsum</button>

      <button
      class="w3-button w3-green w3-round"
      @click="selectedComponent = 'appThirdTab'"
      >Dolor</button>
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
      Velocity(selectedComponent, 'transition.fadeIn', {delay: 1500, duration: 1000}, {complete: done})
    },
    leave(selectedComponent, done) {
      Velocity(selectedComponent, 'transition.slideLeftOut', {duration: 1500}, {complete: done})
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
