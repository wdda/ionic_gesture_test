<template>
  <ion-page>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Blank</ion-title>
        </ion-toolbar>
      </ion-header>
    
      <div id="container">
        <div>Info one: {{ this.infoOne }}</div>
        <div>Info two: {{ this.infoTwo }}</div>

        <div id="controller_one">one</div>
        <div id="controller_two">two</div>
      </div>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar } from '@ionic/vue';
import { defineComponent } from 'vue';
import { createGesture, Gesture } from '@ionic/core'

export default defineComponent({
  name: 'Home',
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar
  },
  mounted () {
    this.$nextTick(() => {
      const one = document.getElementById('controller_one') as HTMLElement

      const gestureOne: Gesture = createGesture({
        el: one,
        threshold: 0,
        disableScroll: true,
        gestureName: 'controller-one',
        onStart: ev => this.onStartOne(ev),
        onEnd: () => this.onEndOne(),
        onMove: ev => this.onMoveOne(ev)
      })

      gestureOne.enable()

      const two = document.getElementById('controller_two') as HTMLElement

      const gestureTwo: Gesture = createGesture({
        el: two,
        threshold: 0,
        disableScroll: true,
        gestureName: 'controller-one',
        onStart: ev => this.onStartTwo(ev),
        onEnd: () => this.onEndTwo(),
        onMove: ev => this.onMoveTwo(ev)
      })

      gestureTwo.enable()
    })
  },
  methods: {
    onStartOne(ev: any) {
      this.infoOne = ev.currentX
    },
    onEndOne() {
      this.infoOne = null
    },
    onMoveOne(ev: any) {
      this.infoOne = ev.currentX
    },
    onStartTwo(ev: any) {
      this.infoTwo = ev.currentX
    },
    onEndTwo() {
      this.infoTwo = null
    },
    onMoveTwo(ev: any) {
      this.infoTwo = ev.currentX
    }
  },
  data() {
    return {
      infoOne: null,
      infoTwo: null,
    }
  }
});
</script>

<style scoped>
#container {
  position: relative;
  height: 100%;
  width: 100%;
}

 #controller_two {
   width: 100px;
   height: 100px;
   position: absolute;
   bottom: 50px;
   right: 50px;
   background-color: #2dd36f;
   z-index: 1;
 }

#controller_one {
  width: 100px;
  height: 100px;
  position: absolute;
  bottom: 50px;
  left: 50px;
  background-color: #2dd36f;
  z-index: 2;
}


</style>