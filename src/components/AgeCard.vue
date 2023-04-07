<template>
  <div class="card">
    <InputGroup v-model="birthdate" :has-error="hasError" />
    <div class="separator">
      <hr />
      <img src="../assets/icon-arrow.svg" alt="" />
    </div>
    <AgeResult :age="age" :has-error="hasError" />
  </div>
</template>

<script lang="ts">
import InputGroup from './InputGroup.vue'
import AgeResult from './AgeResult.vue'

export default {
  components: {
    InputGroup,
    AgeResult,
  },

  data() {
    return {
      birthdate: {
        day: 0,
        month: 0,
        year: 0,
      },
    }
  },

  methods: {
    isValidPastDate(birthdate: date): boolean {
      const MAXIMUM_AGE = 150
      const { day, month, year } = birthdate

      if (!Number.isInteger(+day) || !Number.isInteger(+month) || !Number.isInteger(+year)) {
        return false
      }

      const date = new Date(year, month - 1, day)

      const isPastDate = date.getTime() <= new Date().getTime()
      const isValidDate = date.getDate() === +day && date.getMonth() === +month - 1 && date.getFullYear() === +year

      const ageInMilliseconds = new Date().getTime() - date.getTime()
      const ageInYears = ageInMilliseconds / (1000 * 60 * 60 * 24 * 365.25)
      const isAgeValid = ageInYears <= MAXIMUM_AGE
      console.log(isPastDate, isValidDate, isAgeValid)

      return isValidDate && isPastDate && isAgeValid
    },

    calculateAge(date: date | any): personAge {
      const birthdate = new Date(date.year, date.month - 1, date.day)
      const now = new Date()

      const diff = now.getTime() - birthdate.getTime()

      const years = Math.floor(diff / (1000 * 60 * 60 * 24 * 365.25))
      const months = Math.floor((diff % (1000 * 60 * 60 * 24 * 365.25)) / (1000 * 60 * 60 * 24 * (365.25 / 12)))
      const days = Math.floor((diff % (1000 * 60 * 60 * 24 * (365.25 / 12))) / (1000 * 60 * 60 * 24))

      return { years, months, days }
    },
  },

  computed: {
    age(): personAge {
      if (this.isValidPastDate(this.birthdate)) {
        return this.calculateAge(this.birthdate)
      }

      return {
        years: 0,
        months: 0,
        days: 0,
        hasError: true,
      }
    },
    hasError(): boolean {
      return !this.isValidPastDate(this.birthdate)
    },
  },

  updated() {
    console.log(this.age)
  },
}

interface personAge {
  years: number
  months: number
  days: number
  hasError?: boolean
}

interface date {
  day: number
  month: number
  year: number
}
</script>

<style lang="scss">
.card {
  background-color: white;
  margin: 0 1rem;
  padding: 3.5rem 1.5rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 1rem;
  border-radius: 24px 24px 100px 24px;

  .separator {
    position: relative;
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;

    hr {
      width: 100%;
      position: absolute;
      top: 50%;
      border-color: var(--off-white);
    }
    img {
      z-index: 3;
    }
  }
}

@media (min-width: 840px) {
  .card {
    padding: 4.5rem;
    align-items: flex-start;
    width: 840px;

    .separator {
      align-items: flex-end;

      img {
        width: 96px;
      }
    }
  }
}
</style>
