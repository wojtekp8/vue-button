<script setup lang="ts">
import CustomButton from './components/custom-button.vue';

function handleButtonClick(event: Event) {
  console.log('click', event);
};
</script>

<template>
  <main>
    <div class="btn-wrapper">
      <CustomButton :size="'small'" :type="'outlined'" @click="handleButtonClick">
        Outlined small
      </CustomButton>
      <CustomButton :size="'regular'" :type="'outlined'" @click="handleButtonClick">
        Outlined regular
      </CustomButton>
      <CustomButton :size="'large'" :type="'outlined'" @click="handleButtonClick">
        <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/95/Vue.js_Logo_2.svg/512px-Vue.js_Logo_2.svg.png" alt="Ikona" />
        Outlined + img large
      </CustomButton>
    </div>
    <div class="btn-wrapper">
      <CustomButton :size="'small'"  @click="handleButtonClick">
        Filled small
      </CustomButton>
      <CustomButton :size="'regular'" @click="handleButtonClick">
        <font-awesome-icon icon="fa-solid fa-user" />
        Filled regular
      </CustomButton>
      <CustomButton :size="'large'" @click="handleButtonClick">
        Filled large
      </CustomButton>
    </div>
    <div class="btn-wrapper">
      <CustomButton as="a" :size="'small'"  href="https://google.com">
        As a
      </CustomButton>
      <CustomButton :size="'regular'" @click="handleButtonClick">
        As Button
      </CustomButton>
      <CustomButton :size="'large'" as="router-link" to="./something">
        As router-link
      </CustomButton>
    </div>
    <div class="btn-wrapper">
      <CustomButton :size="'small'" :color="'orange'" @click="handleButtonClick">
        Orange small
      </CustomButton>
      <CustomButton :size="'regular'" :disabled="true" @click="handleButtonClick">
        Disabled regular
      </CustomButton>
      <CustomButton :size="'large'" :color="'green'" @click="handleButtonClick">
        <font-awesome-icon icon="fa-solid fa-heart" />
        Green large
      </CustomButton>
    </div>
    <div class="btn-wrapper">
      <CustomButton :block="true" :color="'green-dark'" @click="handleButtonClick">
        <font-awesome-icon icon="fa-solid fa-cog" />
        Green dark block
      </CustomButton>
    </div>
  </main>
</template>

<style lang="scss" scoped>
main {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  width: 100%;
  max-width: 1200px;

  .btn-wrapper {
    width: 100%;
    margin: 10px 0;
  }
}

</style>
