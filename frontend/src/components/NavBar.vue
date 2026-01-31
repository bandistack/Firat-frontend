<script setup lang="ts">
import '../assets/navbar.css'
import '../assets/color.css'
import '../assets/typography.css'
</script>
<template>
  <nav class="navbar">
    <div class="logo">Firat Frontend</div>
    <ul class="nav-svg">
        <li>

        </li>
    </ul>
  </nav>
</template>
<style scoped>
.navbar{
  width: 100%;   
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: var(--navbar-height-L);
  padding: var(--navbar-padding-L-y) var(--navbar-padding-L-x);
  background-color: var(--color-primary);
  box-sizing: border-box;
  border-bottom: 0.3px solid var(--color-base);
}
.logo{
  font-size: var(--font-size-title-l);
  font-weight: var(--font-weight-title);
  color: var(--color-text);
}
.nav-svg{
  display: flex;
  justify-content: space-between;
}
</style>
