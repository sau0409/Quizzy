<template>
  <nav>
    <div class="nav__logo">
      <h1>Quizzyy</h1>
    </div>
  </nav>
  <router-view />
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Arial, Helvetica, sans-serif;
}
.nav__logo {
  background-image: linear-gradient(to bottom right, rgb(76, 0, 230), rgba(59, 0, 179, 0.8));
  height: 10vh;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  display: flex;
  align-items: center;
  padding-left: 1rem;
}

.nav__logo h1 {
  color: #fff;
  font-weight: bold;
}
</style>
