<template>
  <div>{{ myObject }}</div>
</template>

<script lang="ts">
import Vue from 'vue'
import data from '../externalFile' // Adding the '.ts' file extension will make the --modern build work

export default Vue.extend({
  name: 'IndexPage',
  data: () => ({
    myObject: data
  })
})
</script>
