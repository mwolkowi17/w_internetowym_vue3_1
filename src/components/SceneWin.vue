<script setup>
import { ref,onMounted } from 'vue';

defineOptions({
    inheritAttrs: false
})

defineEmits(['jeszcze-raz', 'koniec-gry']);

onMounted(() => {
    const elementToFocus = document.querySelector(".gram-jeszcze-1")
    if (elementToFocus) {
        elementToFocus.focus();
    }

})

const fanfary = new Audio(new URL('../assets/fanfary.mp3', import.meta.url).href);
fanfary.play();
</script>

<template>
    <div class="plansza-win" role="img" alt="tło" aria-label="Plansza - wygrana"></div>
    <button class="gram-jeszcze-1 anim1" @click="$emit('jeszcze-raz')" role="img" alt="przycisk"
        aria-label="gram jeszcze raz">zagraj jeszcze raz</button>
    <button class="zakoncz-gre anim1" @click="$emit('koniec-gry')" role="img" alt="przycisk"
        aria-label="zakończ grę">zakończ grę</button>
</template>

<style scoped>
.plansza-win {
    background-image: url("../assets/zakonczenie_gry_plansza.png");
    background-size: 1920px 1080px;
    height: 1080px;
    width: 1920px;
    top: 0px;
    left: 0px;
    position: absolute;
    z-index: 2;
}

.gram-jeszcze-1 {
    /* background-image: url("../assets/gram_jeszcze_raz_button.png"); */
     color: rgb(29, 56, 80);
    font-size: 60px;
    font-style: bold;
    font-weight: 700;
    font-family: "Proxima Nova", sans-serif;
    background-size: 583px 192px;
    background-position: -1px -2px;
    position: absolute;
    top: 650px;
    left: 300px;
    width: 583px;
    height: 192px;
    z-index: 3;
    border: 4px solid rgb(0, 187, 255);
}

.gram-jeszcze-1:hover {
    cursor: pointer;
}

.gram-jeszcze-1:focus {
    /* outline: thick double #08e926; */
    outline: 8px solid #08e926;
}

.zakoncz-gre {
    /* background-image: url("../assets/zakoncz_gre_button.png"); */
     color: rgb(29, 56, 80);
    font-size: 60px;
    font-style: bold;
    font-weight: 700;
    font-family: "Proxima Nova", sans-serif;
    background-size: 583px 192px;
    background-position: -1px -2px;
    position: absolute;
    top: 650px;
    left: 1020px;
    width: 583px;
    height: 192px;
    z-index: 3;
    border: 4px solid rgb(0, 187, 255);
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
