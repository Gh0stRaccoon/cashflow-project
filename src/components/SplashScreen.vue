<template>
  <div class="splashscreen">
    <img src="@/assets/logo.svg" alt="Logo" />
    <h1><span>Cash</span>Flow</h1>
  </div>
</template>

<style scoped>
.splashscreen {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  height: 100vh;
}
h1 {
  color: var(--brand-blue);
}
h1 span {
  color: var(--brand-green);
}

img {
  animation: beatit 1.5s ease-in-out infinite alternate;
}

@keyframes beatit {
  from {
    transform: scale(0.9);
  }
  to {
    transform: scale(1);
  }
}
</style>
