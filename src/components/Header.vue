<template>
  <header>
    <img src="@/assets/logo.svg" alt="logo" @click="reload" />
    <h1><span>Cash</span>Flow</h1>
    <span></span>
  </header>
</template>

<script setup>
const reload = () => {
  location.reload();
};
</script>

<style scoped>
header {
  display: flex;
  align-items: center;
  justify-content: space-around;
  width: 100vw;
}

img,
span {
  width: 48px;
}

h1 {
  font-size: 1.4rem;
  color: var(--brand-blue);
}

h1 span {
  color: var(--brand-green);
}
</style>
