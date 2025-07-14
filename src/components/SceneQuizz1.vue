<script setup>
import { ref, onMounted } from 'vue';
import { Quests } from '../lib/quests-source.js';

defineOptions({
  inheritAttrs: false
})

const props = defineProps({
  miejsceNaPlanszy: Number,
  msg: String
});

onMounted(() => {
  const elementToFocus = document.querySelector(".pojedyncza-odpowiedz")
  if (elementToFocus) {
    elementToFocus.focus();
  }

})

const emit = defineEmits(['koniec-quizz',
  'odejmij-szanse']);

let nr_zestawu = Math.floor(Math.random() * 2);

console.log(props.msg);
console.log(props.miejsceNaPlanszy);

const quizz_assets_data = new Quests();



const is_krzyzyk1 = ref(false);
const is_krzyzyk2 = ref(false);
const if_button_dalej = ref(false);
const if_odpowiedz_dobrze = ref(false);
const if_button_dalej_dobrze = ref(false);
const if_odpowiedz_zle = ref(false);
const if_button_dalej_zle = ref(false);
const czy_odpowiedz_poprawna = ref(false);
const czy_odpowiedz_zla = ref(false);

//czy zaznaczone
const zaznaczenieOdpowiedzi1 = ref(false)
const zaznaczenieOdpowiedzi2 = ref(false)


const eksp1 = [
  "planszaQuizz1nr1",
  "planszaQuizz1nr2",
  "planszaQuizz1nr3",
  "planszaQuizz1nr4",
  "planszaQuizz1nr5",
  "planszaQuizz1nr6",
  "planszaQuizz1nr7",
  "planszaQuizz1nr8",
  "planszaQuizz1nr9",
  "planszaQuizz1nr10"
]

function zaznaczenie1() {
  console.log("Zaznaczenie 1");
  if (quizz_assets_data.pokaz_zadanie_2(props.miejsceNaPlanszy).odpowiedz_text[nr_zestawu][2] === 1) {
    console.log("Odpowiedź poprawna");
    czy_odpowiedz_poprawna.value = true;
    czy_odpowiedz_zla.value = false;
    zaznaczenieOdpowiedzi1.value = true
    zaznaczenieOdpowiedzi2.value = false

  } else {
    console.log("Odpowiedź zła");
    czy_odpowiedz_poprawna.value = false;
    czy_odpowiedz_zla.value = true;
    zaznaczenieOdpowiedzi1.value = true
    zaznaczenieOdpowiedzi2.value = false
  }
}

function zaznaczenie2() {
  console.log("Zaznaczenie 2");
  if (quizz_assets_data.pokaz_zadanie_2(props.miejsceNaPlanszy).odpowiedz_text[nr_zestawu][2] === 2) {
    console.log("Odpowiedź poprawna");
    czy_odpowiedz_poprawna.value = true;
    czy_odpowiedz_zla.value = false;
    zaznaczenieOdpowiedzi1.value = false
    zaznaczenieOdpowiedzi2.value = true
  } else {
    console.log("Odpowiedź zła");
    czy_odpowiedz_poprawna.value = false;
    czy_odpowiedz_zla.value = true;
    zaznaczenieOdpowiedzi1.value = false
    zaznaczenieOdpowiedzi2.value = true
  }
}

function sprawdzOdpowiedz() {
  console.log("Sprawdzam odpowiedź");
  if (czy_odpowiedz_poprawna.value) {
    console.log("Odpowiedź poprawna!!!!");
    if_odpowiedz_dobrze.value = true;
    if_button_dalej_dobrze.value = true;
    if_button_dalej.value = false;
    is_krzyzyk1.value = false;
    is_krzyzyk2.value = false;
    const sound_dobrze = new Audio(new URL('../assets/Dobra_odp.mp3', import.meta.url).href);
    sound_dobrze.play()

    const buttonVis = new Promise((resolve, reject) => {
      setTimeout(() => {
        resolve(document.querySelector(".button-dalej-dobrze"))
      }, 300);
    })

    buttonVis.then((res) => { res.focus() })

  } else {
    console.log("Odpowiedź zła!!!!");
    if_odpowiedz_zle.value = true;
    if_button_dalej_zle.value = true;
    if_button_dalej.value = false;
    is_krzyzyk1.value = false;
    is_krzyzyk2.value = false;
    const sound_zle = new Audio(new URL('../assets/zla_odp.mp3', import.meta.url).href);
    sound_zle.play();
    emit('odejmij-szanse');

    const buttonVis2 = new Promise((resolve, reject) => {
      setTimeout(() => {
        resolve(document.querySelector(".button-dalej-dobrze"))
      }, 300);
    })

    buttonVis2.then((res) => { res.focus() })
  }
}

</script>
<template>
  <div class="planszaQuizz1 " :class="eksp1[quizz_assets_data.pokaz_zadanie_2(props.miejsceNaPlanszy).pytanie]"
    role="img" alt="tło" aria-label="pytanie"></div>
  <p class="pytanie1">{{ quizz_assets_data.pokaz_zadanie_2(props.miejsceNaPlanszy).tresc }}</p>

  <ul class="lista-odpowiedzi" role="list">
    <li>
      <!-- <div class="pojedyncza-odpowiedz" role="checkbox" tabindex="0" :aria-checked={zaznaczenieOdpowiedzi1}> -->
      <div class="pojedyncza-odpowiedz" role="checkbox" tabindex="0" :aria-checked="zaznaczenieOdpowiedzi1" @click="is_krzyzyk1 = true,
          is_krzyzyk2 = false,
          if_button_dalej = true,
          zaznaczenie1()" @keydown.enter="is_krzyzyk1 = true,
          is_krzyzyk2 = false,
          if_button_dalej = true,
          zaznaczenie1()" >
        <span class="krzyzyk" :class="{ 'krzyzyk1': is_krzyzyk1, 'krzyzyk2': is_krzyzyk2 }" 
          alt="zaznaczenie odpowiedzi" ></span>
        <span class="pole-zazn pole1 anim1" aria-label="zaznacz odpowiedź 1"></span>

        <span class="odpowiedz odpowiedz1 anim1">{{
          quizz_assets_data.pokaz_zadanie_2(props.miejsceNaPlanszy).odpowiedz_text[nr_zestawu][0] }}</span>
      </div>
    </li>

    <li>
      <!-- <div class="pojedyncza-odpowiedz" role="checkbox" tabindex="0" :aria-checked={zaznaczenieOdpowiedzi1}> -->
      <div class="pojedyncza-odpowiedz" role="checkbox" tabindex="0" :aria-checked="zaznaczenieOdpowiedzi2" @click="is_krzyzyk2 = true,
          is_krzyzyk1 = false,
          if_button_dalej = true,
          zaznaczenie2()" @keydown.enter="is_krzyzyk2 = true,
          is_krzyzyk1 = false,
          if_button_dalej = true,
          zaznaczenie2()">
        <span class="pole-zazn pole2 anim1" aria-label="zaznacz odpowiedź 2"></span>
        <span class="odpowiedz odpowiedz2 anim1">{{
          quizz_assets_data.pokaz_zadanie_2(props.miejsceNaPlanszy).odpowiedz_text[nr_zestawu][1] }}</span>

      </div>
    </li>
  </ul>
  <!-- <div class="krzyzyk" :class="{ 'krzyzyk1': is_krzyzyk1, 'krzyzyk2': is_krzyzyk2 }" role="img"
    alt="zaznaczenie odpowiedzi" aria-label="zaznaczona odpowiedź"></div>
  <button class="pole-zazn pole1 anim1" @click="is_krzyzyk1 = true,
    is_krzyzyk2 = false,
    if_button_dalej = true,
    zaznaczenie1()" role="img" alt="pole zaznaczenia" aria-label="zaznacz odpowiedź 1"></button>

  <p class="odpowiedz odpowiedz1 anim1">{{
    quizz_assets_data.pokaz_zadanie_2(props.miejsceNaPlanszy).odpowiedz_text[nr_zestawu][0] }}</p>
  <button class="pole-zazn pole2 anim1" @click="is_krzyzyk2 = true,
    is_krzyzyk1 = false,
    if_button_dalej = true,
    zaznaczenie2()" role="img" alt="pole zaznaczenia" aria-label="zaznacz odpowiedź 2"></button>
  <p class="odpowiedz odpowiedz2 anim1">{{
    quizz_assets_data.pokaz_zadanie_2(props.miejsceNaPlanszy).odpowiedz_text[nr_zestawu][1] }}</p> -->
  <button class="button-dalej" v-if="if_button_dalej" @click="sprawdzOdpowiedz()" role="button"
    alt="przycisk sprawdź">sprawdź odpowiedź</button>
  <div class="plansza-dobrze" v-if="if_odpowiedz_dobrze">
    <h2 class="naglowek-after-quizz naglowek-dobrze">BRAWO!</h2>
    <h4 class="napis-odpowiedz napis-dobrze">Prawidłowa odpowiedź.</h4>
  </div>
  <button class="button-dalej-dobrze anim1" v-if="if_button_dalej_dobrze" @click="if_odpowiedz_dobrze = false,
    if_button_dalej_dobrze = false,
    $emit('koniec-quizz')" role="button">dalej</button>
  <div class="plansza-zle" v-if="if_odpowiedz_zle">
    <h2 class="naglowek-after-quizz naglowek-zle">Źle!</h2>
    <h4 class="napis-odpowiedz napis-zle">Błędna odpowiedź.</h4>
  </div>
  <button class="button-dalej-dobrze anim1" v-if="if_button_dalej_zle" @click="if_odpowiedz_zle = false,
    if_button_dalej_zle = false,
    $emit('koniec-quizz')" role="button">dalej</button>


</template>
<style scoped>
.planszaQuizz1 {

  background-size: 1411px 896px;
  background-repeat: no-repeat;
  height: 896px;
  width: 1411px;
  position: absolute;
  left: 0px;
  top: 100px;
}

.planszaQuizz1nr1 {
  background-image: url("../assets/pytanie1.png");
}

.planszaQuizz1nr2 {
  background-image: url("../assets/pytanie2.png");
}

.planszaQuizz1nr3 {
  background-image: url("../assets/pytanie3.png");
}

.planszaQuizz1nr4 {
  background-image: url("../assets/pytanie4.png");
}

.planszaQuizz1nr5 {
  background-image: url("../assets/pytanie5.png");
}

.planszaQuizz1nr6 {
  background-image: url("../assets/pytanie6.png");
}

.planszaQuizz1nr7 {
  background-image: url("../assets/pytanie7.png");
}

.planszaQuizz1nr8 {
  background-image: url("../assets/pytanie8.png");
}

.planszaQuizz1nr9 {
  background-image: url("../assets/pytanie9.png");
}

.planszaQuizz1nr10 {
  background-image: url("../assets/pytanie10.png");
}


.pytanie1 {
  color: rgb(29, 56, 80);
  opacity: 0;
  /* tutaj na potrzeby czytnika można dać 0 */
  font-size: 42px;
  font-style: bold;
  font-weight: 700;
  font-family: "Proxima Nova", sans-serif;
  white-space: nowrap;
  position: absolute;
  top: 305px;
  left: 205px;
}

ul {
  display: block;
  margin-block-start: 1em;
  margin-block-end: 1em;
}

li {
  margin-bottom: 20px;
}

.lista-odpowiedzi {
  position: absolute;
  left: 180px;
  top: 455px;
  list-style: none;
}

.pojedyncza-odpowiedz {
  display: flex;
  align-items: center;
  padding: .5rem 1rem;
}

.pojedyncza-odpowiedz:focus {
  outline: 8px solid #9a009e !important;
}

.pole-zazn {
  /* background-image: url("../assets/kratka.png");
  background-size: 50px 50px;
  background-repeat: no-repeat; */
  border: rgb(29, 56, 80) solid 2px;
  height: 81px;
  /* height: 1rem; */
  width: 81px;
  /* width: 1rem; */
  margin-right: 1rem;
  /* position: absolute; */

}

.pole-zazn:hover {
  cursor: pointer;
}

.pole-zazn:focus {
  /* outline: thick double #08e926 !important; */
  outline: 8px solid #9a009e !important;
}

.pole1 {
  /* left: 200px;
  top: 455px; */

}

.pole2 {
  /* left: 200px;
  top: 585px; */
}


.krzyzyk {
  background-image: url("../assets/krzyzyk1.png");
  background-size: 73px 73px;
  background-repeat: no-repeat;
  height: 73px;
  width: 73px;
  position: absolute;
  visibility: hidden;
  z-index: 1;
}

.krzyzyk1 {
  top: 15px;
  left: 62px;
  visibility: visible;
}

.krzyzyk2 {
  top: 135px;
  left: 62px;
  visibility: visible;
}

.odpowiedz {
  color: rgb(29, 56, 80);
  font-size: 42px;
  font-style: bold;
  font-weight: 700;
  font-family: "Proxima Nova", sans-serif;
  white-space: nowrap;
  /* position: absolute; */

}

.odpowiedz1 {
  /* top: 423px;
  left: 300px; */
}

.odpowiedz2 {
  /* top: 552px;
  left: 300px; */
}

.button-dalej {
  background-image: url("../assets/sprawdz_odpwowiedz_button1.png");
  color: rgb(255, 255, 255);
  font-size: 40px;
  font-style: bold;
  font-weight: 700;
  font-family: "Proxima Nova", sans-serif;
  background-size: 394px 87px;
  background-repeat: no-repeat;
  top: 760px;
  left: 300px;
  height: 87px;
  width: 394px;
  position: absolute;
  z-index: 2;
}

.button-dalej:hover {
  cursor: pointer;
}

.button-dalej:focus {
  /* border: 4px solid #08e926; */
  /* outline: thick double #08e926 !important; */
  outline: 8px solid #9a009e !important;
}

.plansza-dobrze {
  background-image: url("../assets/KOMUNIKAT_dobra_odp.png");
  background-size: 1212px 533px;
  background-repeat: no-repeat;
  height: 533px;
  width: 1212px;
  position: absolute;
  left: 83px;
  top: 275px;
}

.plansza-zle {
  background-image: url("../assets/KOMUNIKAT_zla_odp.png");
  background-size: 1212px 533px;
  background-repeat: no-repeat;
  height: 533px;
  width: 1212px;
  position: absolute;
  left: 83px;
  top: 275px;
}

.naglowek-after-quizz {
  color: rgb(255, 255, 255);
  font-size: 100px;
  font-style: bold;
  font-weight: 600;
  font-family: "Proxima Nova", sans-serif;
  top: 5px;

  height: 88px;
  width: 333px;
  position: absolute;
  z-index: 2;
}

.naglowek-dobrze {
  left: 410px;
}

.naglowek-zle {
  left: 520px;
}

.napis-odpowiedz {
  color: rgb(255, 255, 255);
  font-size: 70px;
  font-style: bold;
  font-weight: 400;
  font-family: "Proxima Nova", sans-serif;
  white-space: nowrap;
  top: 115px;

  height: 88px;
  width: 333px;
  position: absolute;
  z-index: 2;
}

.napis-dobrze {
  left: 250px;
}

.napis-zle {
  left: 310px;
}

.button-dalej-dobrze {
  /* background-image: url("../assets/przycisk_dalej_imie.png"); */
  color: rgb(29, 56, 80);
  font-size: 80px;
  font-style: bold;
  font-weight: 700;
  font-family: "Proxima Nova", sans-serif;
  background-size: 301px 117px;
  background-position: -2px -1px;
  background-repeat: no-repeat;
  top: 630px;
  left: 535px;
  height: 117px;
  width: 301px;
  position: absolute;
  z-index: 2;
}

.button-dalej-dobrze:hover {
  cursor: pointer;
}

.button-dalej-dobrze:focus {
  /* border: 4px solid #08e926; */
  /* outline: thick double #08e926 !important; */
  outline: 8px solid #08e926 !important;
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