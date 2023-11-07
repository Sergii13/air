<script setup>
import axios from 'axios'
import { onMounted, ref } from 'vue'

const isLoading = ref(false)
const url = window.location.pathname
const idRegion = ref(url.substring(url.lastIndexOf('/') + 1))

async function getInfo() {
  if (!idRegion.value) {
    idRegion.value = 552
  }
  const result = await axios.get(
    `https://api.gios.gov.pl/pjp-api/rest/station/sensors/${idRegion.value}`
  )
  return result
}

onMounted(() => {
  getInfo()
  console.log(getInfo())
})
</script>
<template>
  <div class="air">
    <div class="air__container">
      <div class="air__result">
        <div class="air__result-item">
          <div class="air__label">Jakość powietrza</div>
          <div class="air__value">123</div>
        </div>
        <div class="air__result-item">
          <div class="air__label">Dwutlenek azotu</div>
          <div class="air__value">123</div>
        </div>
        <div class="air__result-item">
          <div class="air__label">Ozon</div>
          <div class="air__value">123</div>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.air {
  padding: 30px 0;

  & .air__container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
  }

  input {
    background: transparent;
    height: 50px;
    border: 1px solid var(--vt-c-indigo);
    width: 100%;
    padding: 0 20px;
    font-size: 20px;
    max-width: 300px;
    color: var(--vt-c-text-dark-1);
    outline: none;

    &::placeholder {
      color: var(--vt-c-text-dark-1);
    }
  }

  & .air__title {
    text-align: center;
    font-size: 24px;
    margin-bottom: 30px;
  }

  & .air__btn {
    padding: 8px 20px;
    display: inline-flex;
    justify-content: center;
    color: var(--vt-c-text-dark-1);
    align-items: center;
    background: var(--vt-c-indigo);
    margin-top: 20px;
    width: 200px;
    border: none;
    height: 50px;
    font-size: 20px;
    text-transform: capitalize;
  }
}

.air {
  &__result {
  }

  &__result-item {
    display: flex;
    align-items: center;
    font-size: 20px;

    &:not(:last-child) {
      margin-bottom: 20px;
    }
  }

  &__label {
    width: 200px;
  }

  &__value {
  }
}
</style>
