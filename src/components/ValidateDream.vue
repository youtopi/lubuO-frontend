<template>
    <q-card>
      <q-card-title>
        In my dream, the wold..
      </q-card-title>
      <q-card-separator />
        <q-card-main v-if="!edit">
          <big>.. {{currentDream}}</big>
        </q-card-main>
        <q-card-main v-if="edit">
          <q-input v-model="editDream" :placeholder="currentDream" type="textarea" />
        </q-card-main>
        <q-card-separator />
        <q-card-actions align="around" v-if="!edit">
          <q-btn flat round small @click="rejected" color="red"><q-icon name="clear" /></q-btn>
          <q-btn flat round small @click="edit = true" color="blue"><q-icon name="create" /></q-btn>
          <q-btn flat round small @click="accepted" color="green"><q-icon name="done" /></q-btn>
        </q-card-actions>
        <q-card-actions align="around" v-if="edit">
          <q-btn flat round small @click="edit = false" color="reed"><q-icon name="clear" /></q-btn>
          <q-btn flat round small @click="submitChange" color="green"><q-icon name="done" /></q-btn>
        </q-card-actions>
      </q-card>
</template>

<script>

import { Vision } from 'src/api'

import {
  QBtn,
  QCard,
  QCardTitle,
  QCardMedia,
  QCardActions,
  QCardSeparator,
  QCardMain,
  QList,
  QItem,
  QItemMain,
  QItemSide,
  QItemTile,
  QCollapsible,
  QRating,
  QParallax,
  QIcon,
  QPopover,
  QVideo,
  QFab,
  QFabAction,
  QTooltip,
  QFixedPosition,
  Dialog,
  Toast,
  QInput
} from 'quasar'

export default {
  name: 'voteVisionQuestions',
  components: {
    QBtn,
    QCard,
    QCardTitle,
    QCardMedia,
    QCardActions,
    QCardSeparator,
    QCardMain,
    QList,
    QItem,
    QItemMain,
    QItemSide,
    QItemTile,
    QCollapsible,
    QRating,
    QParallax,
    QIcon,
    QPopover,
    QVideo,
    QFab,
    QFabAction,
    QTooltip,
    QFixedPosition,
    Dialog,
    Toast,
    QInput
  },
  data () {
    return {
      edit: false,
      editDream: ''
    }
  },
  created () {
    this.editDream = this.currentDream
  },
  props: ['cardData', 'question'],
  computed: {
    currentDream: function () {
      return this.voteVisionQuestion.vision.text
    },
    voteVisionQuestion: function () {
      return this.question
    }
  },
  methods: {
    submitChange () {
      let vision = new Vision({ text: this.editDream, derivedFromId: this.voteVisionQuestion.vision.id })
      console.log(vision)
      vision.save().then((success) => {
        this.$emit('nextCard')
      })
    },
    accepted () {
      this.voteVisionQuestion.result = true
      this.voteVisionQuestion.save().then((success) => {
        this.$emit('nextCard')
      })
    },
    rejected () {
      this.voteVisionQuestion.result = false
      this.voteVisionQuestion.save().then((success) => {
        this.$emit('nextCard')
      })
    }

  },
  mounted () {
  },
  beforeDestroy () {
  }
}
</script>

<style lang="stylus">
</style>
