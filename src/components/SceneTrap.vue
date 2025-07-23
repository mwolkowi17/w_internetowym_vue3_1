<script setup>
import { ref, onMounted } from 'vue';

defineEmits(['koniec-pulapka','koniec-pulapka-focus']);

defineOptions({
  inheritAttrs: false
})

const props = defineProps({
    ifButtonOnFocusTrap: Boolean
})

onMounted(() => {
  const elementToFocus = document.querySelector(".przycisk_pulapka1")
  if (elementToFocus&&props.ifButtonOnFocusTrap===true) {
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
    <p class="naglowek">ZASADZKA!</p>
    <p class="napis">Cofasz się o dwa pola.</p>
  </div>
  <button class="przycisk_pulapka1 my-button anim1" @click="$emit('koniec-pulapka'); koniecPulapki()" @keydown.enter="$emit('koniec-pulapka-focus')" role="button">dalej</button>
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

.naglowek {
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

.napis {
  color: rgb(255, 255, 255);
  font-size: 70px;
  font-style: bold;
  font-weight: 400;
  font-family: "Proxima Nova", sans-serif;
  white-space: nowrap;
  top: 140px;
  left: 280px;
  height: 88px;
  width: 333px;
  position: absolute;
  z-index: 2;
}

.my-button{
  transition: .2s ease-out;
}

.my-button::after {
  content: '';
  position: absolute;
  left: 0;
  top: 0;
  inset: 0;
  height: 130%;
  width: 110%;
  box-sizing: border-box;

}

.my-button:hover {
  cursor: pointer;
  transform: scale(1.1);
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
  outline: 5px solid #08e926;
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