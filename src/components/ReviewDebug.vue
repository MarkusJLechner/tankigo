<template>
  <div
    v-if="card"
    class="fixed right-0 bottom-32 left-0 z-20 -mt-3 h-64 overflow-y-auto bg-black/60 px-6 text-xs opacity-90 backdrop-blur-xs"
  >
    <div class="text-yellow-500">Deck ID: {{ deck.id }}</div>
    <div class="mb-1 text-yellow-400">Deck Name: {{ deck.name }}</div>
    <div class="font-bold text-blue-300">Card:</div>
    <div>id: {{ card.id }}</div>
    <div>nid: {{ card.nid }}</div>
    <div>did: {{ card.did }}</div>
    <div>ord: {{ card.ord }}</div>
    <div>mod: {{ card.mod }}</div>
    <div>mod: {{ new Date(card.mod * 1000).toLocaleString() }}</div>
    <div>usn: {{ card.usn }}</div>
    <div>type: {{ card.type }}</div>
    <div>cardType: {{ card.cardType }}</div>
    <div>queue: {{ card.queue }}</div>
    <div>queueType: {{ card.queueType }}</div>
    <div>due: {{ card.due }}</div>
    <div>due: {{ new Date(card.due).toLocaleString() }}</div>
    <Promise :promise="card.dueDate">
      <template #default="{ result }">
        <div>dueDate: {{ result?.toLocaleString() }}</div>
      </template>
    </Promise>
    <div>ivl: {{ card.ivl }}</div>
    <div>factor: {{ card.factor }}</div>
    <div>reps: {{ card.reps }}</div>
    <div>lapses: {{ card.lapses }}</div>
    <div>left: {{ card.left }}</div>
    <div>odue: {{ card.odue }}</div>
    <div>odid: {{ card.odid }}</div>
    <div>flags: {{ card.flags }}</div>
    <div>data: {{ card.data }}</div>
    <div class="font-bold text-blue-300">NOTE:</div>
    <div v-if="note">
      <div v-html="getFields().join(' ')"></div>
      <div>Tags: {{ note.tags }}</div>
      <div>flags: {{ note.flags }}</div>
      <div>usn: {{ note.usn }}</div>
      <div>csum: {{ note.csum }}</div>
      <div>mid: {{ note.mid }}</div>
      <div>mod: {{ note.mod }}</div>
      <div>mod: {{ new Date(card.mod * 1000).toLocaleString() }}</div>
      <Promise :promise="card.model">
        <template #default="{ result: model, loading }">
          <div class="font-bold text-blue-300">MODEL:</div>
          <div v-if="loading">loading</div>
          <div v-else>
            <div>id: {{ model.id }}</div>
            <div>vers: {{ model.vers }}</div>
            <div>name: {{ model.name }}</div>
            <div>tags: {{ model.tags }}</div>
            <div>did: {{ model.did }}</div>
            <div>usn: {{ model.usn }}</div>
            <div>req: {{ model.req }}</div>
            <div>flds: {{ model.flds }}</div>
            <div>sortf: {{ model.sortf }}</div>
            <div>tmpls: {{ model.tmpls }}</div>
            <div>mod: {{ model.mod }}</div>
            <div>latexPost: {{ model.latexPost }}</div>
            <div>type: {{ model.type }}</div>
            <div>css: {{ model.css }}</div>
            <div>latexPre: {{ model.latexPre }}</div>
          </div>
        </template>
      </Promise>
    </div>
    <div class="font-bold text-blue-300">DECK:</div>
    <div v-if="deck">
      <div>browserCollapsed: {{ deck.browserCollapsed }}</div>
      <div>collapsed: {{ deck.collapsed }}</div>
      <div>conf: {{ deck.conf }}</div>
      <div>desc: {{ deck.desc }}</div>
      <div>dyn: {{ deck.dyn }}</div>
      <div>extendNew: {{ deck.extendNew }}</div>
      <div>extendRev: {{ deck.extendRev }}</div>
      <div>id: {{ deck.id }}</div>
      <div>lrnToday: {{ deck.lrnToday }}</div>
      <div>mod: {{ deck.mod }}</div>
      <div>mod: {{ new Date(deck.mod * 1000).toLocaleString() }}</div>
      <div>name: {{ deck.name }}</div>
      <div>newToday: {{ deck.newToday }}</div>
      <div>revToday: {{ deck.revToday }}</div>
      <div>timeToday: {{ deck.timeToday }}</div>
      <div>usn: {{ deck.usn }}</div>
    </div>
  </div>
</template>

<script setup lang="ts">
import Promise from '@/components/Promise.vue'

interface Props {
  card?: Record<string, any> | null
  note?: Record<string, any> | null
  deck?: Record<string, any> | null
}

const props = withDefaults(defineProps<Props>(), {
  card: null,
  note: null,
  deck: null,
})

function getFields(): string[] {
  if (!props.note) {
    return []
  }

  return props.note.flds.split('\u001f')
}
</script>

<style scoped></style>
