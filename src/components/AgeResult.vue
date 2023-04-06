<script lang="ts">
export default {
  props: {
    age: {
      type: Object,
      required: true,
    },
    hasError: {
      type: Boolean,
      required: true,
    },
  },

  methods: {
    getValue(value?: number) {
      if (this.hasError || (!value && value != 0)) {
        return '- -'
      }

      return value
    },
  },
}
</script>

<template>
  <div class="results">
    <div class="result-item">
      <span class="number">{{ getValue(age.years) }}</span> years
    </div>

    <div class="result-item">
      <span class="number">{{ getValue(age.months) }}</span> months
    </div>

    <div class="result-item">
      <span class="number">{{ getValue(age.days) }}</span> days
    </div>
  </div>
</template>

<style lang="scss" scoped>
.results {
  font-size: 3.5rem;
  color: var(--off-black);
  font-weight: 800;
  font-style: italic;

  .number {
    font-weight: 900;
    color: var(--purple);
  }
}

@media (min-width: 840px) {
  .results {
    font-size: 6rem;
    line-height: 6.5rem;
  }
}
</style>
