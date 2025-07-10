<script setup>
import { ref, onMounted } from 'vue';
defineEmits(['wybor-levelu1']);

onMounted(() => {
    const elementToFocus = document.querySelector(".level-one-button")
    if (elementToFocus) {
        elementToFocus.focus();
    }

})
</script>

<template>
    <div class="tlo-level1" role="img" alt="tło" aria-label="Wybór poziomu">
        <button class="level-one-button" @click="$emit('wybor-levelu1')" role="img" alt="przycisk"
            aria-label="Przycisk poziom jeden" autofocus>poziom 1</button>
        <button class="level-two-button" role="img" alt="przycisk" aria-label="Przycisk poziom dwa nieaktywny"
            disabled>poziom 2</button>
    </div>
</template>

<style scoped>
.tlo-level1 {
    background-image: url("../assets/plansza_poziom1_wybor.png");
    background-size: 1920px 1080px;
    height: 1080px;
    width: 1920px;
    top: 0px;
    left: 0px;
    position: absolute;
}

.level-one-button {
    color: rgb(29, 56, 80);
    font-size: 100px;
    font-style: bold;
    font-weight: 700;
    font-family: "Proxima Nova", sans-serif;
    /* background-image: url("../assets/poziom1_button.png"); */
    background-size: 595px 200px;
    background-position: -1px -1px;
    position: absolute;
    top: 438px;
    left: 220px;
    width: 595px;
    height: 200px;
     border: 4px solid rgb(0, 187, 255);
}

.level-one-button:hover {
    cursor: pointer;
}

.level-one-button:focus {
    /* outline: thick double #08e926; */
    outline: 8px solid #08e926;
}

.level-two-button {
    color: rgb(29, 56, 80);
    font-size: 100px;
    font-style: bold;
    font-weight: 700;
    font-family: "Proxima Nova", sans-serif;
    /* background-image: url("../assets/poziom2_nieaktywny_popr.png"); */
    background-size: 595px 200px;
    background-position: -2px -1px;
    position: absolute;
    top: 438px;
    left: 1063px;
    width: 595px;
    height: 200px;
     border: 4px solid rgb(0, 187, 255);
}
</style>