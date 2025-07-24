<script setup>
import { ref, onMounted } from 'vue'
import { instrukcjaTekst } from '../lib/instrukcja';
defineEmits(['koniec-instrukcja', 'koniec-instrukcja-focus'])

const props = defineProps({
  ifButtonOnFocus: Boolean
});

onMounted(() => {
  const elementToFocus = document.querySelector(".dalej")
  //dodanie warunku propsu
  if (elementToFocus && props.ifButtonOnFocus === true) {
    elementToFocus.focus();
  }

})

const textToDisplay ="Znajdujesz się w Wirtualnej Dżungli - aby ją przejść, musisz odpowiedzieć "+
       " prawidłowo na pytania dotyczące internetu. Gra składa się z dwóch"+
        " poziomów. Rzucasz kostką i posuwasz się do przodu o tyle pól, ile oczek"+
        " wyrzuciła kostka. Na początku gry otrzymujesz trzy szanse.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"+
        " Na polach oznaczonych znakiem zapytania &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; czeka Cię pytanie." + 
        " Każda błędna odpowiedź - to strata 1 szansy. Utrata wszystkich szans" + 
        " oznacza zakończenie gry. Dobra odpowiedź - to kolejny rzut kostką" + 
        " Po drodze czekają Cię zasadzki kryjące się na polach oznaczonych" + 
        " wykrzyknikiem &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;. Powodzenia!"
</script>
<template>
  <div class="tlo1" aria-label="Zasady gry">
    <h1 class="instrukcja-title">Zasady gry</h1>
    <div class="kontener-instrukcja">
      <!-- <p class="instrukcja">
        Znajdujesz się w Wirtualnej Dżungli - aby ją przejść, musisz odpowiedzieć 
        prawidłowo na pytania dotyczące internetu. Gra składa się z dwóch
        poziomów. Rzucasz kostką i posuwasz się do przodu o tyle pól, ile oczek
        wyrzuciła kostka. Na początku gry otrzymujesz trzy szanse.
        Na polach oznaczonych znakiem zapytania czeka Cię pytanie.
        Każda błędna odpowiedź - to strata 1 szansy. Utrata wszystkich szans
        oznacza zakończenie gry. Dobra odpowiedź - to kolejny rzut kostką
        Po drodze czekają Cię zasadzki kryjące się na polach oznaczonych
        wykrzyknikiem. Powodzenia!
      </p> -->
         <p class="instrukcja" v-html="textToDisplay"></p>
         <img class="gwiazdka" src="../assets/ikona1gwiazdka.png" />
         <img class="pytajnik" src="../assets/ikona2question.png"/>
         <img class="wykrzyknik" src="../assets/ikona3wykrzyknik.png" />
    </div>
  </div>
  <button class="dalej anim1" @click="$emit('koniec-instrukcja')" @keydown.enter="$emit('koniec-instrukcja-focus')"
    role="button">Dalej</button>

</template>

<style scoped>
.tlo1 {
  background-image: url("../assets/plansza_zasady_gry.png");
  background-size: 1920px 1080px;
  height: 1080px;
  width: 1920px;
  top: 0px;
  left: 0px;
  position: absolute;
}
.instrukcja-title{
  position: absolute;
    color: rgb(255, 255, 255);
  font-size: 110px;
  font-style: normal;
  font-weight: 400;
  font-family: "Proxima Nova", sans-serif;
  line-height: 1.5;
  top: 20px;
  left: 705px;
}

.kontener-instrukcja {
  display: flex;
  align-items: center;
  padding: .5rem 1rem;
  /* width: 1300px; */
  width: 1400px;
  top: 210px;
  left: 260px;
  position: absolute;
}

.instrukcja {
  color: rgb(255, 255, 255);
  font-size: 41px;
  font-style: normal;
  font-weight: 300;
  font-family: "Proxima Nova", sans-serif;
  line-height: 1.5;
  position: relative;

}

.gwiazdka{
  position: absolute;
  top: 220px;
  left: 746px;
}

.pytajnik{
  position: absolute;
   top: 283px;
  left: 355px;
}

.wykrzyknik{
  position: absolute;
  top: 475px;
  left: 715px;
}

.my-button {
  transition: .2s ease-out;
  /* overflow: visible; */
}

/* .my-button::after {
  content: '';
  position: absolute;
  left: 0;
  top: 0;
  inset: 0;
  height: 130%;
  width: 110%;
  box-sizing: border-box;

} */

.my-button:hover {
  cursor: pointer;
  transform: scale(1.03);
}

.dalej {
  /* background-image: url("../assets/przycisk_dalej_imie.png"); */
  color: rgb(29, 56, 80);
  font-size: 70px;
  font-style: bold;
  font-weight: 700;
  font-family: "Proxima Nova", sans-serif;
  position: absolute;
  top: 800px;
  left: 850px;
  width: 301px;
  height: 117px;
  border: 4px solid rgb(0, 187, 255);
  /* display: flex;
  align-items: center;
  justify-content: center;
  box-sizing: border-box;
  overflow: hidden;           /* Prevent overflow *
  transform-origin: center;  */
  transition: .2s ease-in-out;

}

.dalej:hover {
  cursor: pointer;
  transform: scale(1.1);
}

.dalej:focus {
  /* border: 4px solid #08e926; */
  /* outline: thick double #08e926; */
  outline: 5px solid #08e926;
}

/* The animation code */
@keyframes example {

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