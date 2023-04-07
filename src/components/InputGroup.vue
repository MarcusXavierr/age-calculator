<script lang="ts">
export default {
  props: ['modelValue', 'hasError'],
  emits: ['update:modelValue'],
  mounted() {
    console.log(this.modelValue)
  },
}
</script>

<template>
  <div class="input-container" :class="hasError && 'has-error'">
    <div class="input-group">
      <label for="day">DAY</label>
      <input
        type="text"
        :value="modelValue.day || null"
        @input="modelValue.day = $event.target?.value"
        placeholder="DD"
      />
    </div>
    <div class="input-group">
      <label for="month">MONTH</label>
      <input
        type="text"
        :value="modelValue.month || null"
        @input="modelValue.month = $event.target?.value"
        placeholder="MM"
      />
    </div>
    <div class="input-group">
      <label for="year">YEAR</label>
      <input
        :value="modelValue.year || null"
        @input="modelValue.year = $event.target?.value"
        type="text"
        placeholder="YYYY"
      />
    </div>
  </div>
</template>

<style lang="scss" scoped>
.input-container {
  display: flex;
  gap: 1rem;
}

.input-group {
  flex-grow: 1;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

label {
  font-weight: 800;
  letter-spacing: 0.35rem;
  color: var(--smokey-grey);
}

input {
  font-size: 1.5rem;
  border: 1px solid var(--light-grey);
  padding: 0.75rem 1rem;
  border-radius: 0.5rem;
  font-weight: 700;
  width: 5.5rem;
}

.has-error {
  label {
    color: red;
  }

  input {
    border-color: red;
  }
}

@media (min-width: 840px) {
  input {
    width: 10rem;
    font-size: 2rem;
  }
}
</style>
