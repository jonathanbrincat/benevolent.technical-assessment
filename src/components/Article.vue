<template>
  <article class="bg-white text-slate-700 border border-neutral-200 rounded-sm">
    <header class="border-b border-neutral-200 flex items-center justify-between py-4 px-6">
      <h2 class="text-xl font-semibold">{{ item.name }}</h2>
      <template v-if="item.triageStatus === TRIAGE_STATUS.NOT_MATCH">
        <Badge :message="triageStatusDictionary[TRIAGE_STATUS.NOT_MATCH]" status="failure" />
      </template>
      <template v-else-if="item.triageStatus === TRIAGE_STATUS.MATCH">
        <Badge :message="triageStatusDictionary[TRIAGE_STATUS.MATCH]" status="success" />
      </template>
    </header>

    <div class="py-2 px-6">
      <table class="w-full border-separate border-spacing-y-4">
        <tbody>
          <tr>
            <td>Safety:</td>
            <td class="text-right">{{ item.safety }}</td>
          </tr>
          <tr>
            <td>Novely:</td>
            <td class="text-right">{{ item.novelty }}</td>
          </tr>
          <tr>
            <td>Efficacy:</td>
            <td class="text-right">{{ item.efficacy }}</td>
          </tr>
          <tr>
            <td>Total score:</td>
            <td class="text-right">{{ sum(item.safety, item.novelty, item.efficacy) }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </article>
</template>

<script setup>
import Badge from './Badge.vue'

defineProps({
  item: {
    type: Object,
    required: true
  }
})

const TRIAGE_STATUS = {
  UNKNOWN: 'UNKNOWN',
  NOT_MATCH: 'NOT_MATCH',
  MATCH: 'MATCH',
}

const triageStatusDictionary = {
  UNKNOWN: 'Not match',
  NOT_MATCH: 'Not match',
  MATCH: 'Match',
}

const sum = (...n) => n.reduce((accumulator, current) => accumulator + current, 0)
</script>