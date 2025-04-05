<template>
  <div id="app">
    <Header @navigate="currentPage = $event" />
    <transition name="fade" mode="out-in">
      <main class="main-content" :key="currentPage">
        <!-- Hero Section -->
        <section v-if="currentPage === 'home'" class="hero">
          <h1></h1>
          <p>
            สวัสดีพ่อแม่พี่น้องทุกท่าน
          </p>
        </section>

        <!-- About Section -->
        <AboutSection v-if="currentPage === 'about'" />

        <!-- Education Section -->
        <EducationSection v-if="currentPage === 'education'" />

        <!-- Contact Section -->
        <ContactSection v-if="currentPage === 'contact'" />
      </main>
    </transition>
  </div>
</template>

<script>
import Header from './components/HeaderSection.vue';
import EducationSection from './components/EducationSection.vue';
import AboutSection from './components/AboutSection.vue';
import ContactSection from './components/ContactSection.vue';

export default {
  name: 'App',
  components: {
    Header,
    EducationSection,
    AboutSection,
    ContactSection
  },
  data() {
    return {
      currentPage: 'home', // Default page
    };
  },
};
</script>

<style>
body {
  margin: 0;
  font-family: 'Inter', sans-serif;
  background-image: url('@/assets/images/12.jpg');
  background-size: cover;
  background-position: center;
  color: #333;
}


#app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.main-content {
  flex: 1;
  padding: 2rem;
  max-width: 960px;
  margin: 0 auto;
}

.hero {
  text-align: center;
  margin-bottom: 3rem;
}

.hero h1 {
  font-size: 2.5rem;
  font-weight: 600;
  margin-bottom: 1rem;
}

.hero p {
  font-size: 1.2rem;
  color: #555;
}

.contact {
  text-align: center;
}

.contact h1 {
  font-size: 2.5rem;
  font-weight: 600;
  margin-bottom: 1rem;
}

.contact p {
  font-size: 1.2rem;
  color: #555;
}


/* Animation */
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s ease;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
</style>