<script setup>
import { ref, onMounted } from 'vue';
import { metodyPomocnicze } from '../lib/metody-pomocnicze';
import { PawnMaps } from '../lib/pawn-maps';
import { Traps } from "../lib/traps";
import SceneTrap from './SceneTrap.vue';
import SceneQuizz2 from './SceneQuizz2.vue';


defineOptions({
    inheritAttrs: false
})
const emit = defineEmits(['koniec-etap2', 'przegrana2', 'koniec-etap2-focus', 'przegrana2-focus'])

const props = defineProps({
    ifButtonOnFocusMain2: Boolean
})



//obsługa focusa
const ifQuizzFocusOn2 = ref(false)
const ifTrapFocusOn = ref(false)
const ifRzucKostkaButtonOnFocus = ref(false)
const ifFocusEmitGlobal = ref(false)

onMounted(() => {
    const elementToFocus = document.querySelector(".rzut2")
    if (elementToFocus && props.ifButtonOnFocusMain2 === true) {
        elementToFocus.focus();
    }

})
//roboczo tylko dla starej funkcji
const postac1 = ref("postać")

//pozycja startowa gracza nr 1
const krok_gracz1_na_planszy = ref(0);
//roboczo do edycji quizów
//const krok_gracz1_na_planszy = ref(15);

//zdefinowanie pozycji (mapy wszystkich pozycji) gracza nr 1
const pozycje_pionka_gracza1 = new PawnMaps().pionek_gracza1;

//początkowa ilość "szans"
const ilosc_szans = ref(4);

//widoczność przycisku Rzuć kostką
const if_rzuc_kostka = ref(true)

//widoczność kostki 
const if_widok_kostki = ref(false);

//widoczność planszy pułapka
const if_widok_pulapki = ref(false);

//widoczność planszy quizz1
const if_widok_quizz2 = ref(false);
//roboczo do edycji quizów
//const if_widok_quizz2 = ref(true); 

//widoki szans na planszy

const if_szansa1 = ref(true)
const if_szansa2 = ref(true)
const if_szansa3 = ref(true)
const if_szansa4 = ref(true)

//const obrazek_kostki = ref('../assets/kostka_1oczko.png')

let kolekcja_widoków_kostki = [
    false,
    false,
    false,
    false,
    false,
    false,
]

const isSet1 = ref(kolekcja_widoków_kostki[0])
const isSet2 = ref(kolekcja_widoków_kostki[1])
const isSet3 = ref(kolekcja_widoków_kostki[2])
const isSet4 = ref(kolekcja_widoków_kostki[3])
const isSet5 = ref(kolekcja_widoków_kostki[4])
const isSet6 = ref(kolekcja_widoków_kostki[5])

//pozycja pionka
const pionek_left = ref(30)
const pionek_top = ref(330)

const mapa_pozycji_pionka = new PawnMaps()

//flaga true/false pokazująca czy gracz nr 1 nie przeszedł całej planszy, wartość falsce wskazuje zakończenie ruchu na planszy
let kontrolka_ruch_na_planszy = true;

// licznik ruchu na planszy - faktyczny ruch pionka
let ruch_lokalny = 0;

let x;

const wyrzuconaWartoscKostki = ref("Kostka - liczba oczek: " + (x + 1));

function kostka_click() {

    if_rzuc_kostka.value = false //  ukryj przycisk rzuć kostką
    //========================================================================================
    let i = 0; //  set your counter to 0
    //========================================================================================
    if_widok_kostki.value = true
    console.log("rzut")
    x = metodyPomocnicze.rzucaj();
    wyrzuconaWartoscKostki.value = "Kostka - liczba oczek: " + (x + 1);
    let wynik_rzutu = x
    console.log(x)
    for (let i = 0; i < 6; i++) {
        if (i === x) {
            kolekcja_widoków_kostki[i] = true
        }
        else {
            kolekcja_widoków_kostki[i] = false
        }


        isSet1.value = kolekcja_widoków_kostki[0]
        isSet2.value = kolekcja_widoków_kostki[1]
        isSet3.value = kolekcja_widoków_kostki[2]
        isSet4.value = kolekcja_widoków_kostki[3]
        isSet5.value = kolekcja_widoków_kostki[4]
        isSet6.value = kolekcja_widoków_kostki[5]


    }

    console.log(kolekcja_widoków_kostki)

    //!!============================ruch pionka loop =========================================
    const myLoopPionek = (arg_A, arg_B, arg_C) => {
        //  create a loop function
        setTimeout(function () {
            //  call a 1s setTimeout when the loop is called

            pionek_left.value = arg_B[arg_C.value + i][0]
            pionek_top.value = arg_B[arg_C.value + i][1]

            //console.log(arg_B)
            console.log(arg_C.value)
            console.log(arg_B[arg_C.value + i])



            //arg_A.setPosition(arg_B[arg_C + i][0], arg_B[arg_C + i][1]);

            if (ruch_lokalny >= 15) {
                console.log("Zwycięstwo!");
                kontrolka_ruch_na_planszy = false;
                console.log("wygrałeś!!!");
                wywolanie_sceny_koncowej();
            }


            ruch_lokalny++;

            i++; //  increment the counter

            // if (i <= wynik_rzutu && ruch_lokalny <= 15) {
            if (i <= wynik_rzutu && ruch_lokalny <= 15) {
                myLoopPionek(arg_A, arg_B, arg_C); //  ..  again which will trigger another                         
            } else {
                dodanie_krokow();
                pulapka_czy_quizz();
            }


            //  ..  setTimeout()

        }, 1000);
    };


    function dodanie_krokow() {
        krok_gracz1_na_planszy.value =
            krok_gracz1_na_planszy.value + wynik_rzutu + 1;
    }


    if (kontrolka_ruch_na_planszy === true) {
        //  start the loop
        myLoopPionek(
            postac1,
            pozycje_pionka_gracza1,
            krok_gracz1_na_planszy,

        )

        console.log("krok na planszy: " + krok_gracz1_na_planszy.value);
    }

    //instancja obieku odpowiadającego za pułapki
    const trap = new Traps();

    const pulapka_czy_quizz = () => {
        console.log("sprawdzam czy pułapka albo quizz");
        console.log(i)
        console.log("wynik rzutu: " + wynik_rzutu);
        console.log("kontrolka ruch na planszy: " + kontrolka_ruch_na_planszy);
        //if (i === (wynik_rzutu+1) && kontrolka_ruch_na_planszy === true) {
        if (kontrolka_ruch_na_planszy === true) {
            console.log("pulapka albo quizz!!!");
            console.log("krok gracza na planszy: " + krok_gracz1_na_planszy.value);
            // sprawdzenie czy gracz wpadł w pułapkę
            console.log(trap.czy_polapka(krok_gracz1_na_planszy.value));
            //  tu w momencie kiedy gracz zanjdzie się na polu pułapka będzie go cofało a jak nie to odpala quizz
            if (trap.czy_polapka(krok_gracz1_na_planszy.value) === true) {
                console.log("wpadka");
                //  pokazuje planszę pułapki
                setTimeout(() => {
                    if_widok_pulapki.value = true;
                    const sound_cofasz = new Audio(new URL('../assets/zla_odp.mp3', import.meta.url).href);
                    sound_cofasz.play();
                }, 1000)

            } else {
                console.log("quiz");
                setTimeout(() => {
                    if_widok_quizz2.value = true
                }, 1000);
            }
        }
    };

    const wywolanie_sceny_koncowej = () => {
        console.log("wywołanie sceny końcowej");
        if (ifFocusEmitGlobal.value === false) {
            emit('koniec-etap2')
        }
        if (ifFocusEmitGlobal.value === true) {
            emit('koniec-etap2-focus')
        }
    };


}

const koniecQuizu = () => {
    if_rzuc_kostka.value = true

    const buttonRzutVis = new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve(document.querySelector(".rzut2"))
        }, 300);
    })

    //buttonRzutVis.then((res) => { res.focus() })
}

const koniecQuizuFocusOn = () => {
    if_rzuc_kostka.value = true

    const buttonRzutVis = new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve(document.querySelector(".rzut2"))
        }, 300);
    })

    buttonRzutVis.then((res) => { res.focus() })
}

const koniecPulapki = () => {
    console.log("emmiter - krok do tyłu");
    console.log(krok_gracz1_na_planszy.value);
    krok_gracz1_na_planszy.value = krok_gracz1_na_planszy.value - 2;
    ruch_lokalny = ruch_lokalny - 2;
    console.log(krok_gracz1_na_planszy.value);
    pionek_left.value = pozycje_pionka_gracza1[krok_gracz1_na_planszy.value - 1][0]
    pionek_top.value = pozycje_pionka_gracza1[krok_gracz1_na_planszy.value - 1][1]
    if_rzuc_kostka.value = true;

    // const buttonRzutVis = new Promise((resolve, reject) => {
    //     setTimeout(() => {
    //         resolve(document.querySelector(".rzut2"))
    //     }, 300);
    // })

    // buttonRzutVis.then((res) => { res.focus() })
}

const koniecPulapkiFocusOn = () => {
    console.log("emmiter - krok do tyłu");
    console.log(krok_gracz1_na_planszy.value);
    krok_gracz1_na_planszy.value = krok_gracz1_na_planszy.value - 2;
    ruch_lokalny = ruch_lokalny - 2;
    console.log(krok_gracz1_na_planszy.value);
    pionek_left.value = pozycje_pionka_gracza1[krok_gracz1_na_planszy.value - 1][0]
    pionek_top.value = pozycje_pionka_gracza1[krok_gracz1_na_planszy.value - 1][1]
    if_rzuc_kostka.value = true;

    const buttonRzutVis = new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve(document.querySelector(".rzut2"))
        }, 300);
    })

    buttonRzutVis.then((res) => { res.focus() })
}

const odejmijSzanse = () => {
    console.log("odejmij szanse");
    ilosc_szans.value = ilosc_szans.value - 1;

    console.log("ilosc_szans:" + ilosc_szans.value);

    if (ilosc_szans.value === 3) {
        if_szansa4.value = false;
    }
    if (ilosc_szans.value === 2) {
        if_szansa3.value = false;
    }
    if (ilosc_szans.value === 1) {
        if_szansa2.value = false;
        console.log("przegrałeś!!!");
    }
    if (ilosc_szans.value === 0) {
        if_szansa1.value = false;
        console.log("przegrałeś!!!");
        if_widok_quizz2.value = false;
        if (ifFocusEmitGlobal.value === false) {
            emit('przegrana2');
        }
        if (ifFocusEmitGlobal.value === true) {
            emit('przegrana2-focus')
        }
    }
}

function clickWithFocus() {
    ifQuizzFocusOn2.value = true
    ifTrapFocusOn.value = true
    ifFocusEmitGlobal.value = true
    kostka_click()
}

function clickWithMouse() {
    ifFocusEmitGlobal.value = false
    kostka_click()
}
</script>
<template>
    <div class="tlo_main2" role="img" alt="tło" aria-label="gra planszowa - poziom 2"></div>
    <div class="pionek1" :style="{ left: pionek_left + 'px', top: pionek_top + 'px' }" role="img" alt="pionek"
        aria-label="Pionek"></div>
    <h3 class="szanse-napis">szanse:</h3>
    <div class="szansa1 szansa_ksztalt1" v-if="if_szansa1" role="img" alt="gwiazdka ikona szansy" aria-label="Szansa 1">
    </div>
    <div class="szansa2 szansa_ksztalt1" v-if="if_szansa2" role="img" alt="gwiazdka ikona szansy" aria-label="Szansa 2">
    </div>
    <div class="szansa3 szansa_ksztalt1" v-if="if_szansa3" role="img" alt="gwiazdka ikona szansy" aria-label="Szansa 3">
    </div>
    <div class="szansa4 szansa_ksztalt1" v-if="if_szansa4" role="img" alt="gwiazdka ikona szansy" aria-label="Szansa 4">
    </div>
    <button class="rzut2 my-button anim1" v-if="if_rzuc_kostka" @click="clickWithMouse" @keydown.enter="clickWithFocus"
        role="button">Rzut kostką</button>
    <div class="kostka1" :class="{
        'kostka1image1': isSet1,
        'kostka1image2': isSet2,
        'kostka1image3': isSet3,
        'kostka1image4': isSet4,
        'kostka1image5': isSet5,
        'kostka1image6': isSet6
    }" v-if="if_widok_kostki" role="img" alt="kostka do gry" :aria-label=wyrzuconaWartoscKostki></div>
    <SceneTrap v-if="if_widok_pulapki" @koniec-pulapka="if_widok_pulapki = false, koniecPulapki()"
        @koniec-pulapka-focus="if_widok_pulapki = false; koniecPulapkiFocusOn()" rel="preload"
        :ifButtonOnFocusTrap="ifTrapFocusOn" />
    <SceneQuizz2 v-if="if_widok_quizz2" @koniec-quizz="if_widok_quizz2 = false, koniecQuizu()"
        @koniec-quizz-focus="if_widok_quizz2 = false, koniecQuizuFocusOn()" @odejmij-szanse="odejmijSzanse" msg="Hej"
        :miejsceNaPlanszy="krok_gracz1_na_planszy" :ifButtonOnFocusQuizz2="ifQuizzFocusOn2" rel="preload" />
</template>

<style scoped>
.tlo_main2 {
    background-image: url("../assets/8_plansza_poziom2.png");
    background-size: 1920px 1080px;
    height: 1080px;
    width: 1920px;
    top: 0px;
    left: 0px;
    position: absolute;
}

.pionek1 {
    background-image: url("../assets/pionek1.png");
    background-size: 116px 116px;
    background-repeat: no-repeat;
    height: 116px;
    width: 116px;
    position: absolute;

}

.szanse-napis {
    color: rgb(29, 56, 80);
    font-size: 45px;
    font-style: bold;
    font-weight: 600;
    font-family: "Proxima Nova", sans-serif;

    top: 255px;
    left: 1465px;
    height: 88px;
    width: 333px;
    position: absolute;
    z-index: 2;
}

.kostka1 {

    background-size: 250px 250px;
    background-repeat: no-repeat;
    left: 1549px;
    top: 687px;
    height: 250px;
    width: 250px;
    position: absolute;
    z-index: 2;
}

.kostka1image1 {
    background-image: url("../assets/kostka_1oczko.png");
}

.kostka1image2 {
    background-image: url("../assets/kostka_2oczka.png");
}

.kostka1image3 {
    background-image: url("../assets/kostka_3oczka.png");
}

.kostka1image4 {
    background-image: url("../assets/kostka_4oczka.png");
}

.kostka1image5 {
    background-image: url("../assets/kostka_5oczek.png");
}

.kostka1image6 {
    background-image: url("../assets/kostka_6oczek.png");
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

.rzut2 {
    color: rgb(255, 255, 255);
    font-size: 40px;
    font-style: bold;
    font-weight: 700;
    font-family: "Proxima Nova", sans-serif;
    background-image: url("../assets/rzut_przycisk.png");
    background-size: 333px 86px;
    background-repeat: no-repeat;
    top: 560px;
    left: 1502px;
    height: 88px;
    width: 333px;
    position: absolute;
    z-index: 2;
}

.rzut2:hover {
    cursor: pointer;
}

.rzut2:focus {
    /* outline: thick double #08e926; */
    outline: 5px solid #9a009e;
}

.szansa_ksztalt1 {
    background-image: url("../assets/zycie1.png");
    background-size: 72px 72px;
    background-repeat: no-repeat;

    height: 72px;
    width: 72px;
    position: absolute;
    z-index: 2;
}

.szansa1 {
    top: 387px;
    left: 1490px;
}

.szansa2 {
    top: 387px;
    left: 1590px;
}

.szansa3 {
    top: 387px;
    left: 1690px;
}

.szansa4 {
    top: 387px;
    left: 1790px;
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

/*anim1* The element to apply the animation to */
.anim1 {

    animation-name: example;
    animation-duration: 1s;
}
</style>