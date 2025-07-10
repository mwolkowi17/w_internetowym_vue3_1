<script setup>
import { ref, onMounted } from 'vue';
defineEmits(['jeszcze-raz','koniec-gry']);

onMounted(() => {
    const elementToFocus = document.querySelector(".gram-jeszcze-1")
    if (elementToFocus) {
        elementToFocus.focus();
    }

})

const przegrana_sound = new Audio(new URL('../assets/przegrana_gra.mp3', import.meta.url).href);
przegrana_sound.play();
</script>

<template>
    <div class="plansza-lose" role="img" alt="tło" aria-label="Plansza - przegrana"></div>
    <button class="gram-jeszcze-1 anim1" @click="$emit('jeszcze-raz')" role="img" alt="przycisk" aria-label="gram jeszcze raz"></button>
    <button class="zakoncz-gre anim1" @click="$emit('koniec-gry')" role="img" alt="przycisk" aria-label="zakończ grę"></button>
</template>

<style scoped>
.plansza-lose {
    background-image: url("../assets/przegrana_plansza.png");
    background-size: 1920px 1080px;
    height: 1080px;
    width: 1920px;
    top: 0px;
    left: 0px;
    position: absolute;
    z-index: 2;
}
.gram-jeszcze-1{
    background-image: url("../assets/gram_jeszcze_raz_button.png");
     background-size: 583px 192px;
    background-position: -1px -2px;
    position: absolute;
    top: 650px;
    left: 300px;
    width: 583px;
    height: 192px;
    z-index: 3;
}

.gram-jeszcze-1:hover {
    cursor: pointer;
}
.gram-jeszcze-1:focus {
    /* outline: thick double #08e926; */
    outline: 8px solid #08e926;
}
.zakoncz-gre{
    background-image: url("../assets/zakoncz_gre_button.png");
   background-size: 583px 192px;
    background-position: -1px -2px;
    position: absolute;
    top: 650px;
    left: 1020px;
    width: 583px;
    height: 192px;
    z-index: 3;
}
.zakoncz-gre:hover {
    cursor: pointer;
}

.zakoncz-gre:focus {
    /* outline: thick double #08e926; */
    outline: 8px solid #08e926;
}
/* The animation code */
@keyframes example {
  /* from {background-color: red;}
  to {background-color: yellow;} */
  from {opacity: 0;}
  to {opacity: 100;}
}

/* The element to apply the animation to */
.anim1 {
  
  animation-name: example;
  animation-duration: 1s;
}
</style>