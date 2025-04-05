<template>
  <header class="navbar">
    <a href="#" class="logo" @click.prevent="$emit('navigate', 'home')">MY PORTFOLIO</a>
    <div class="navbar-right">
      <a href="#about" @click.prevent="$emit('navigate', 'about')">ABOUT</a>
      <a href="#education" @click.prevent="$emit('navigate', 'education')">EDUCATION</a>
      <a href="#contact" @click.prevent="$emit('navigate', 'contact')">CONTACT</a>
    </div>
  </header>
</template>

<style scoped>
/* ฟอนต์แบบ modern */
body {
  margin: 0;
  font-family: 'Inter', sans-serif;
  background-color: #fff;
  color: #111;
}

/* Navbar */
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 28px 40px;
  background-color: #fff;
  border-bottom: 1px solid #eee;
  position: sticky;
  top: 0;
  z-index: 999;
}

/* Logo ฝั่งซ้าย */
.logo {
  font-size: 1.2rem;
  font-weight: 600;
  color: #111;
  text-decoration: none;
  letter-spacing: 0.5px;
}

/* เมนูฝั่งขวา */
.navbar-right a {
  margin-left: 30px;
  text-decoration: none;
  color: #111;
  font-weight: 400;
  font-size: 1rem;
  transition: opacity 0.2s ease;
}

.navbar-right a:hover {
  opacity: 0.6;
}

/* Responsive */
@media (max-width: 768px) {
  .navbar {
    flex-direction: column;
    align-items: flex-start;
    padding: 20px;
  }

  .navbar-right {
    margin-top: 10px;
    display: flex;
    flex-direction: column;
    gap: 10px;
  }

  .navbar-right a {
    margin-left: 0;
  }
}
</style>