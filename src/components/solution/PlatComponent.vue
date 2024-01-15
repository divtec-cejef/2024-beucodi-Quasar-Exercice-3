<template>
<q-card
  class="card">
  <q-img
    :src="plat.image"
    basic
    contain
  >
    <div class="absolute-bottom text-h6">
      {{ plat.nom }}
    </div>
  </q-img>

  <q-card-section>
    <q-rating
      readonly
      :model-value="plat.note"
      size="2em"
      color="orange"
      class="q-mt-sm"
    />
  </q-card-section>

  <q-card-section class="description">
    <span v-if="plat.description">{{ plat.description }}</span>
    <i v-else>Aucune descripion fournie.</i>
  </q-card-section>

  <q-card-actions
    class="absolute-bottom"
    align="right">
    <q-btn
      @click="afficherFormPlat = true"
      icon="edit"
      color="blue"
      flat>Modifier</q-btn>
    <q-btn
      @click="dialogSupprimer"
      icon="delete"
      color="red"
      flat>Supprimer</q-btn>
  </q-card-actions>

  <q-dialog
    v-model="afficherFormPlat">
    <form-plat
      action="modifier"
      :platAModifier="plat"
      @close="afficherFormPlat = false" />
  </q-dialog>

</q-card>
</template>

<script setup>
import { useSolutionPlatsStore } from 'stores/solutionPlats'
import { ref } from 'vue'
import { Dialog } from 'quasar'
import FormPlat from 'components/Solution/FormPlat.vue'

const { plat } = defineProps(['plat'])
const afficherFormPlat = ref(false)

const store = useSolutionPlatsStore()

const dialogSupprimer = () => {
  Dialog.create({
    title: 'Supprimer plat',
    message: 'Voulez-vous supprimer ce plat ?',
    persistent: true,
    ok: {
      label: 'Supprimer',
      push: true
    },
    cancel: {
      label: 'Annuler',
      push: true,
      color: 'grey'
    }
  }).onOk(() => {
    store.supprimerPlat(plat.id)
  })
}
</script>

<style>
.card {
  min-height: 400px;
  max-width: 250px;
  width: 250px;
  transition: background 0.3s;
}
.card-clickable {
  cursor: pointer;
}
.card-clickable:hover {
  background: #bdbdbd!important;
}
.card .q-img {
  max-height: 180px;
}
.card .q-img__image {
  background-size: cover !important;
}
.card .q-rating__icon {
  opacity: 0.2;
}
.card .q-rating__icon--active {
  opacity: 1;
}
.card .description {
  padding: 5px 16px;
}
</style>
