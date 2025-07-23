<script setup>
import { onMounted } from 'vue';

const props = defineProps({
 ifButtonOnFocus: Boolean
});

onMounted(() => {
    const elementToFocus = document.querySelector(".gram-jeszcze-1-level-one")
    if (elementToFocus&&props.ifButtonOnFocus===true) {
        elementToFocus.focus();
    }
})

defineEmits(['gram-dalej','gram-dalej-focus', 'koniec-gry', 'koniec-gry-focus']);

const fanfary = new Audio(new URL('../assets/fanfary.mp3', import.meta.url).href);
fanfary.play();
</script>

<template>
    <div class="plansza-win-level-one">
        <p class="naglowek">BRAWO!</p>
        <p class="napis">Udało ci się ukończyć <b>Poziom 1</b></p>
        <p class="napis-2">Chcesz grać dalej?</p>
    </div>
    <button class="gram-jeszcze-1-level-one anim1" @click="$emit('gram-dalej')" @keydown.enter="$emit('gram-dalej-focus')" role="button">gram dalej</button>
    <button class="zakoncz-gre anim1" @click="$emit('koniec-gry')" @keydown.enter="$emit('koniec-gry-focus')" role="button">zakończ grę</button>

</template>

<style scoped>
.plansza-win-level-one {
    background-image: url("../assets/ukonczenie_poziomu1.png");
    background-size: 1920px 1080px;
    height: 1080px;
    width: 1920px;
    top: 0px;
    left: 0px;
    position: absolute;
    z-index: 2;
}

.naglowek {
    color: rgb(255, 255, 255);
    font-size: 100px;
    font-style: bold;
    font-weight: 600;
    font-family: "Proxima Nova", sans-serif;
    top: 140px;
    left: 780px;
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
    top: 290px;
    left: 480px;
    height: 88px;
    width: 333px;
    position: absolute;
    z-index: 2;
}

.napis-2 {
    color: rgb(255, 255, 255);
    font-size: 70px;
    font-style: bold;
    font-weight: 400;
    font-family: "Proxima Nova", sans-serif;
    white-space: nowrap;
    top: 380px;
    left: 660px;
    height: 88px;
    width: 333px;
    position: absolute;
    z-index: 2;
}

.gram-jeszcze-1-level-one {
    /* background-image: url("../assets/gram_dalej1.png"); */
    color: rgb(29, 56, 80);
    font-size: 80px;
    font-style: bold;
    font-weight: 700;
    font-family: "Proxima Nova", sans-serif;
    background-size: 583px 192px;
    background-position: -1px -1px;
    position: absolute;
    top: 650px;
    left: 280px;
    width: 583px;
    height: 192px;
    z-index: 3;
    border: 4px solid rgb(0, 187, 255);
}

.gram-jeszcze-1-level-one:hover {
    cursor: pointer;
}

.gram-jeszcze-1-level-one:focus {
    /* outline: thick double #08e926; */
    outline: 5px solid #08e926;
}

.zakoncz-gre {
    /* background-image: url("../assets/zakoncz_gre_button.png"); */
    color: rgb(29, 56, 80);
    font-size: 80px;
    font-style: bold;
    font-weight: 700;
    font-family: "Proxima Nova", sans-serif;
    background-size: 583px 192px;
    background-position: -1px -1px;
    position: absolute;
    top: 650px;
    left: 980px;
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