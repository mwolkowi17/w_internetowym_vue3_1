<script setup>
import { ref, onMounted } from 'vue';

defineEmits(['koniec-pulapka']);

defineOptions({
  inheritAttrs: false
})

onMounted(() => {
  const elementToFocus = document.querySelector(".przycisk_pulapka1")
  if (elementToFocus) {
    elementToFocus.focus();
  }

})

function koniecPulapki() {

  // Emit the event to notify the parent component that the trap has ended
  console.log("Koniec pulapki");

}


</script>
<template>
  <div class="pulapka1">
    <h2 class="naglowek">ZASADZKA!</h2>
       <h4 class="napis">Cofasz się o dwa pola.</h4>
  </div>
  <button class="przycisk_pulapka1 anim1" @click="$emit('koniec-pulapka'); koniecPulapki()" role="button"
    alt="ikona dalej">dalej</button>
</template>
<style scoped>
.pulapka1 {
  background-image: url("../assets/zasadzka.png");
  background-size: 1212px 533px;
  background-repeat: no-repeat;
  height: 533px;
  width: 1212px;
  position: absolute;
  left: 100px;
  top: 250px;
}

.naglowek{
color: rgb(255, 255, 255);
  font-size: 100px;
  font-style: bold;
  font-weight: 600;
  font-family: "Proxima Nova", sans-serif;
  top: 5px;
  left: 350px;
  height: 88px;
  width: 333px;
  position: absolute;
  z-index: 2;
 
}

.napis{
color: rgb(255, 255, 255);
  font-size: 70px;
  font-style: bold;
  font-weight: 400;
  font-family: "Proxima Nova", sans-serif;
  white-space: nowrap;
  top: 110px;
  left: 280px;
  height: 88px;
  width: 333px;
  position: absolute;
  z-index: 2;
}

.przycisk_pulapka1 {
  /* background-image: url("../assets/przycisk_dalej_imie.png"); */
  color: rgb(29, 56, 80);
  font-size: 80px;
  font-style: bold;
  font-weight: 700;
  font-family: "Proxima Nova", sans-serif;
  background-size: 301px 117px;
  background-position: -1px -2px;
  background-repeat: no-repeat;
  height: 117px;
  width: 301px;
  position: absolute;
  left: 545px;
  top: 590px;
  border: 4px solid rgb(0, 187, 255);

}

.przycisk_pulapka1:hover {
  cursor: pointer;
}

.przycisk_pulapka1:focus {
  /* outline: thick double #08e926; */
  outline: 8px solid #08e926;
}

/* The animation code */
@keyframes example {

  /* from {background-color: red;}
  to {background-color: yellow;} */
  from {
    opacity: 0;
  }

  to {
    opacity: 100;
  }
}

/* The element to apply the animation to */
.anim1 {

  animation-name: example;
  animation-duration: 1s;
}
</style>