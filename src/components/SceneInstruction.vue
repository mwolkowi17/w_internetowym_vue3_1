<script setup>
import { ref,onMounted } from 'vue'
import { instrukcjaTekst } from '../lib/instrukcja';
defineEmits(['koniec-instrukcja'])

onMounted(() => {
 const elementToFocus = document.querySelector(".dalej")
 if (elementToFocus) {
      elementToFocus.focus();
    }

})
</script>
<template>
 <div class="tlo1" role="img" alt="tło" :aria-label="instrukcjaTekst"  ></div>
<button class="dalej anim1" @click="$emit('koniec-instrukcja')" role="img" alt="przycisk" aria-label="Przycisk dalej" ></button>
</template>
<style>
.tlo1{
    background-image: url("../assets/plansza_zasady_gry.png");
    background-size: 1920px 1080px;
    height: 1080px;
    width: 1920px;
    top:0px;
    left: 0px;
    position: absolute;
}
.dalej{
    background-image: url("../assets/przycisk_dalej_imie.png");
    background-size: 301px 117px;
    background-position: -1px -1px;
    position: absolute;
    top: 820px;
    left: 850px;
    width: 301px;
    height: 117px;
}
.dalej:hover{
    cursor: pointer;
}

.dalej:focus {
   /* border: 4px solid #08e926; */
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