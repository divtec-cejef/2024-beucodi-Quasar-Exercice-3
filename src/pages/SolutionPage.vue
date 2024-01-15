<template>
<q-page class="q-pa-lg">
  <div class="row q-gutter-lg">

    <PlatComponent
      v-for="plat in plats"
      :key="plat.id"
      :plat="plat" />

    <BoutonAjouter
      @click="afficherFormPlat = true" />

    <q-dialog
      v-model="afficherFormPlat">
      <FormPlat
        @close="afficherFormPlat = false"
        action="ajouter" />
    </q-dialog>

  </div>
</q-page>
</template>

<script setup>
import { ref } from 'vue'
import PlatComponent from 'components/Solution/PlatComponent.vue'
import BoutonAjouter from 'components/Solution/BoutonAjouter.vue'
import FormPlat from 'components/Solution/FormPlat.vue'
import { useSolutionPlatsStore } from 'stores/solutionPlats'

const store = useSolutionPlatsStore()

const afficherFormPlat = ref(false)
const plats = store.plats
</script>
