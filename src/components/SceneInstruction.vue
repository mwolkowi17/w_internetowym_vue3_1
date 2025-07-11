<script setup>
import { ref, onMounted } from 'vue'
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
  <div class="tlo1" aria-label="Zasady gry">
    <p class="instrukcja">
      Znajdujesz się w Wirtualnej Dżungli - aby ją przejść, musisz odpowiedzieć <br>
      prawidłowo na pytania dotyczące internetu. Gra składa się z dwóch<br>
      poziomów. Rzucasz kostką i posuwasz się do przodu o tyle pól, ile oczek<br>
      wyrzuciła kostka. Na początku gry otrzymujesz trzy szanse.<br>
      Na polach oznaczonych znakiem zapytania czeka cię pytanie.<br>
      Każda błędna odpowiedź - to strata 1 szansy. Utrata wszystkich szans<br>
      oznacza zakończenie gry. Dobra odpowiedź - to kolejny rzut kostką<br>
      Po drodze czekają Cię zasadzki kryjące się na polach oznaczonych<br>
      wykrzykniknikiem. Powodzenia!
    </p>
    </div>
    <button class="dalej anim1" @click="$emit('koniec-instrukcja')" role="button" alt="przycisk"
      aria-label="Przycisk dalej">dalej</button>
  
</template>
<style>
.tlo1 {
  background-image: url("../assets/plansza_zasady_gry.png");
  background-size: 1920px 1080px;
  height: 1080px;
  width: 1920px;
  top: 0px;
  left: 0px;
  position: absolute;
}

.instrukcja{
  color: rgb(255, 255, 255);
  font-size: 41px;
  font-style: bold;
  font-weight: 600;
  font-family: "Proxima Nova", sans-serif;
   position: absolute;
  top: 260px;
  left: 310px;
}

.dalej {
  /* background-image: url("../assets/przycisk_dalej_imie.png"); */
  color: rgb(29, 56, 80);
  font-size: 70px;
  font-style: bold;
  font-weight: 700;
  font-family: "Proxima Nova", sans-serif;
  background-size: 301px 117px;
  background-position: -1px -1px;
  position: absolute;
  top: 800px;
  left: 850px;
  width: 301px;
  height: 117px;
  border: 4px solid rgb(0, 187, 255);
}

.dalej:hover {
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