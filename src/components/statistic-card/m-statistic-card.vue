<script lang="ts">
export default {
  props: {
    icon: {
      type: String,
      required: true,
    },
    statistic: {
      type: [String],
      required: true,
    },
    statisticTitle: {
      type: String,
      default: '',
    },
    color: {
      type: String,
      default: 'primary',
    },
  },
}
</script>

<template>
  <VRow>
    <VCol>
      <CardStatisticsVerticalSimple
        :icon="icon"
        :title="statisticTitle"
        :color="color"
        :stats="statistic"
      />
    </VCol>
  </VRow>
</template>
