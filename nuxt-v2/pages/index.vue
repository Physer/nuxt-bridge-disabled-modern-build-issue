<template>
  <div>{{ myObject }}</div>
</template>

<script lang="ts">
import Vue from 'vue'
import data from '../externalFile'

export default Vue.extend({
  name: 'IndexPage',
  data: () => ({
    myObject: data
  })
})
</script>
