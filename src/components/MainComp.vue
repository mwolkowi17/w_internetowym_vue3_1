<script setup>
import { ref, onMounted } from 'vue'
import ScenaStart from './ScenaStart.vue'
import SceneInstruction from './SceneInstruction.vue'
import SceneMain1 from './SceneMain1.vue';
import SceneMain2 from './SceneMain2.vue';
import SceneLevelOneChoise from './SceneLevelOneChoise.vue';
import SceneLevelTwoChoise from './SceneLevelTwoChoise.vue';
import SceneWin from './SceneWin.vue';
import SceneLoose from './SceneLoose.vue';
import SceneLooseAfterLevelOne from './SceneLooseAfterLevelOne.vue';
import SceneEndLevelOne from './SceneEndLevelOne.vue';
import { images } from '../lib/image-list';
import { preloadImages } from '../lib/preloader';

const if_plansza_poczatkowa = ref(false)
const if_instrukcja = ref(false)
const if_end_scene_level_one = ref(false)
const if_level_one_choise = ref(false)
const if_level_two_choise = ref(false)
const if_main1 = ref(false)
const if_main2 = ref(true)
const if_win = ref(false)
const if_loose = ref(false)
const if_loose_after_level_one = ref(false)

//sterowanie widokami gry
function change() {
    if_plansza_poczatkowa.value = false;
    if_instrukcja.value = true;
}

function change_instrukcja() {
    if_instrukcja.value = false
    if_level_one_choise.value = true
}

function change_level_one_choise() {
    console.log("wybrano level 1")
    if_end_scene_level_one.value=false;
    if_loose_after_level_one.value=false
    if_level_one_choise.value = false;
    if_level_two_choise.value = false;
    if_main2.value=false
    if_main1.value = true;
}

function change_level_two_choise() {
    console.log("wybrano poziom 2")
    if_level_one_choise.value = false;
    if_level_two_choise.value = false;
    if_main1.value = false;
    if_main2.value = true;
}

function koniec_etapu1() {


    if (if_main1.value) {
        if_main1.value = true;
        //if_level_two_choise.value = true;
        
        if_end_scene_level_one.value = true;
    } else {
        if_win.value = true;
    }
}

function loose() {
    if_loose.value = true;
}

function loose_after_level_one() {
    if_loose_after_level_one.value = true;
  
}

function graj_dalej_po_scenie1() {
    console.log('graj_dalej_po_scenie1')
    if_main1.value = false;
    if_end_scene_level_one.value = false;
    if_level_two_choise.value = true;
  
}
function graj_jeszcze_raz() {
    console.log('graj_jeszcze_raz')
    if_loose.value = false;
    if_win.value = false;
    if_main1.value = false;
    if_main2.value = false;
    if_level_two_choise.value = true
}
function graj_jeszcze_raz_po_scenie1() {
    console.log('graj_jeszcze_raz po scenie1')
    if_loose_after_level_one.value = false;
    if_end_scene_level_one.value=false
    if_win.value = false;
    if_main1.value = false;
    if_main2.value = false;
    if_level_one_choise.value = true
}

function koniec_gry() {
    console.log('koniec_gry')
    if_loose.value = false;
    if_win.value = false;
    if_main1.value = false;
    if_main2.value = false;
    if_level_two_choise.value = false;
    if_end_scene_level_one.value = false;
    if_loose_after_level_one.value=false;
    if_plansza_poczatkowa.value = true;
}


// preload images
const newImages = ref([])

onMounted(async () => {
    await preloadImages(images)
  
    newImages.value = images
})

</script>


<template>
    <div>
        <ScenaStart v-if="if_plansza_poczatkowa" @koniec-planszy="change()" />
        <SceneInstruction v-if="if_instrukcja" @koniec-instrukcja="change_instrukcja()" />
        <SceneLevelOneChoise v-if="if_level_one_choise" @wybor-levelu1="change_level_one_choise" />
        <SceneLevelTwoChoise v-if="if_level_two_choise" @wybor-levelu1="change_level_one_choise"
            @wybor-levelu2="change_level_two_choise" />
        <SceneMain1 v-if="if_main1" @koniec-etap1="koniec_etapu1" @przegrana="loose_after_level_one" />
        <SceneEndLevelOne v-if="if_end_scene_level_one" @gram-dalej="graj_dalej_po_scenie1" @koniec-gry="koniec_gry" />
        <SceneMain2 v-if="if_main2" @koniec-etap2="koniec_etapu1" @przegrana2="loose" />
        <SceneWin v-if="if_win" @jeszcze-raz="graj_jeszcze_raz" @koniec-gry="koniec_gry" />
        <SceneLoose v-if="if_loose" @jeszcze-raz="graj_jeszcze_raz" @koniec-gry="koniec_gry" />
        <SceneLooseAfterLevelOne v-if="if_loose_after_level_one" @jeszcze-raz="graj_jeszcze_raz_po_scenie1"
            @koniec-gry="koniec_gry" />
    </div>
</template>

<style scoped>
.tytul {
    color: greenyellow;
}




.start:hover {
    cursor: pointer;
}
</style>