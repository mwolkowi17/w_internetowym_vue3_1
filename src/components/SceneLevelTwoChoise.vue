<script setup>
import { ref, onMounted} from 'vue';
defineEmits(['wybor-levelu1','wybor-levelu2']);

onMounted(() => {
 const elementToFocus = document.querySelector(".level-one-button")
 if (elementToFocus) {
      elementToFocus.focus();
    }

})
</script>
<template>
<div class="tlo-level2" role="img" alt="tło" aria-label="plansza wyboru poziomu"></div>
   <button class="level-one-button" @click="$emit('wybor-levelu1')" role="img" alt="przycisk" aria-label="wybierz poziom jeden"></button>
   <button class="level-two-button" @click="$emit('wybor-levelu2')" role="img" alt="przycisk" aria-label="wybierz poziom dwa"></button>
</template>
<style scoped>
.tlo-level2 {
 background-image: url("../assets/plansza_poziom1_wybor.png");
    background-size: 1920px 1080px;
    height: 1080px;
    width: 1920px;
    top:0px;
    left: 0px;
    position: absolute;
}

.level-one-button {
   background-image: url("../assets/poziom1_button.png");
    background-size: 595px 200px;
    background-position: -1px -1px;
    position: absolute;
    top: 438px;
    left: 220px;
    width: 595px;
    height: 200px;
}
.level-one-button:hover {
    cursor: pointer;
}
.level-one-button:focus {
    /* outline: thick double #08e926; */
    outline: 8px solid #08e926;
}

.level-two-button{
    background-image: url("../assets/poziom2_button.png");
     background-size: 595px 200px;
    background-position: -2px -1px;
    position: absolute;
   top: 438px;
    left: 1063px;
    width: 595px;
    height: 200px;
}

.level-two-button:hover {
    cursor: pointer;
}
.level-two-button:focus {
    /* outline: thick double #08e926; */
    outline: 8px solid #08e926;
}
</style>