<template>
  <div class="contact-container">
    <h2 class="contact-heading">Contact Me</h2>
    <div class="contact-cards">
      <!-- Email -->
      <div class="contact-card email-card">
        <div class="icon-container">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="icon">
            <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"></path>
            <polyline points="22,6 12,13 2,6"></polyline>
          </svg>
        </div>
        <div class="contact-info">
          <h3>Email</h3>
          <a href="mailto:poramet.han@ku.th">poramet.han@ku.th</a>
        </div>
      </div>

      <!-- Facebook -->
      <div class="contact-card facebook-card">
        <div class="icon-container">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="icon">
            <path d="M18 2h-3a4 4 0 0 0-4 4v3H8v4h3v8h4v-8h3l1-4h-4V6a1 1 0 0 1 1-1h3z"></path>
          </svg>
        </div>
        <div class="contact-info">
          <h3>Facebook</h3>
          <a href="https://www.facebook.com/feelbored/?viewas=100000686899395" target="_blank">Poramet Hanfa</a>
        </div>
      </div>

      <!-- Instagram -->
      <div class="contact-card instagram-card">
        <div class="icon-container">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="icon">
            <rect x="2" y="2" width="20" height="20" rx="5" ry="5"></rect>
            <path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"></path>
            <line x1="17.5" y1="6.5" x2="17.5" y2="6.5"></line>
          </svg>
        </div>
        <div class="contact-info">
          <h3>Instagram</h3>
          <a href="https://www.instagram.com/besttt_q/" target="_blank">besttt_q</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ContactSection",
};
</script>

<style scoped>
.contact-container {
  padding: 2rem;
  max-width: 800px;
  margin: 0 auto;
}

.contact-heading {
  text-align: center;
  font-size: 2rem;
  margin-bottom: 2rem;
  color: #333;
}

.contact-cards {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.contact-card {
  background: #f9f9f9;
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 1rem;
  display: flex;
  align-items: center;
  transition: box-shadow 0.2s ease;
}

.contact-card:hover {
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.icon-container {
  width: 50px;
  height: 50px;
  background: #eaeaea;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-right: 1rem;
}

.icon {
  width: 24px;
  height: 24px;
  color: #555;
}

.contact-info h3 {
  margin: 0;
  font-size: 1.1rem;
  color: #333;
}

.contact-info a {
  font-size: 0.9rem;
  color: #555;
  text-decoration: none;
}

.contact-info a:hover {
  text-decoration: underline;
}
</style>