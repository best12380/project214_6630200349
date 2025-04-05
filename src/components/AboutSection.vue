<template>
  <section class="about-section">
    <div class="about-container">
      <!-- Left Section: Profile Picture Carousel -->
      <div class="about-left">
        <div class="carousel">
          <div
            class="carousel-images"
            :style="{ transform: `translateX(-${currentIndex * 100}%)` }"
          >
            <img
              v-for="(image, index) in profileImages"
              :key="index"
              :src="image"
              class="profile-image"
            />
          </div>
        </div>
      </div>

      <!-- Right Section: Personal Information -->
      <div class="about-right">
        <h1>{{ fullName }}</h1>
        <p><strong>Student ID:</strong> {{ studentId }}</p>
        <p><strong>Major:</strong> {{ major }}</p>
        <p><strong>Previous School:</strong> {{ previousSchool }}</p>
        <div class="quote">
          <blockquote>
            "{{ quote }}"
          </blockquote>
        </div>
        <button @click="openModal" class="edit-button">Edit</button>
      </div>
    </div>

    <!-- Popup Modal -->
    <div v-if="showModal" class="modal-overlay">
      <div class="modal">
        <h2>Edit Information</h2>
        <form @submit.prevent="saveInfo">
          <label>
            Full Name:
            <input v-model="form.fullName" type="text" required />
          </label>
          <label>
            Student ID:
            <input v-model="form.studentId" type="text" required />
          </label>
          <label>
            Major:
            <input v-model="form.major" type="text" required />
          </label>
          <label>
            Previous School:
            <input v-model="form.previousSchool" type="text" required />
          </label>
          <label>
            Quote:
            <textarea v-model="form.quote" rows="3" required></textarea>
          </label>
          <label>
            Add Profile Image:
            <input type="file" @change="onFileChange" accept="image/*" multiple />
          </label>
          <div class="modal-actions">
            <button type="submit" class="save-button">Save</button>
            <button type="button" @click="closeModal" class="cancel-button">Cancel</button>
          </div>
        </form>
      </div>
    </div>
  </section>
</template>

<script>

export default {
  name: "AboutSection",
  data() {
    return {
      profileImages: [
        require("@/assets/images/1270e12c64500c4b4b217be1a60337b0.jpg"),
        require("@/assets/images/artworks-000201806104-c4px4h-t1080x1080.jpg"),
        require("@/assets/images/mitsuki-koga-v0-pzl93pl5htyd1.webp"),
      ],
      currentIndex: 0,
      fullName: "Poramet Hanfa",
      studentId: "6630200349",
      major: "Computer Science",
      previousSchool: "Kasetsart University",
      quote: "Lost in a world that doesn’t exist.-bestsupersus",
      showModal: false,
      form: {
        profileImages: [],
        fullName: "",
        studentId: "",
        major: "",
        previousSchool: "",
        quote: "",
      },
    };
  },
  mounted() {
    this.startAutoSlide();
  },
  beforeUnmount() {
    clearInterval(this.autoSlideInterval);
  },
  methods: {
    startAutoSlide() {
      this.autoSlideInterval = setInterval(() => {
        this.nextImage();
      }, 3000); // Change image every 3 seconds
    },
    nextImage() {
      this.currentIndex = (this.currentIndex + 1) % this.profileImages.length;
    },
    onFileChange(event) {
      const files = event.target.files;
      Array.from(files).forEach((file) => {
        const reader = new FileReader();
        reader.onload = (e) => {
          this.profileImages.push(e.target.result);
        };
        reader.readAsDataURL(file);
      });
    },
    openModal() {
      this.form = {
        profileImages: this.profileImages,
        fullName: this.fullName,
        studentId: this.studentId,
        major: this.major,
        previousSchool: this.previousSchool,
        quote: this.quote,
      };
      this.showModal = true;
    },
    closeModal() {
      this.showModal = false;
    },
    saveInfo() {
      this.profileImages = this.form.profileImages.length
        ? this.form.profileImages
        : this.profileImages;
      this.fullName = this.form.fullName;
      this.studentId = this.form.studentId;
      this.major = this.form.major;
      this.previousSchool = this.form.previousSchool;
      this.quote = this.form.quote;
      this.closeModal();
    },
  },
};
</script>

<style scoped>
.about-section {
  max-width: 1200px;
  margin: 0 auto;
  padding: 80px 20px;
  font-family: 'Inter', 'Helvetica Neue', sans-serif;
  color: #111;
  line-height: 1.8;
  background-color: #ffffffd0;
  border-radius: 12px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.06);
  animation: fadeIn 1s ease-in;
}

@keyframes fadeIn {
  0% {
    opacity: 0;
    transform: translateY(30px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}

.about-container {
  display: flex;
  gap: 20px;
  align-items: center;
  flex-wrap: wrap;
}

.carousel {
  position: relative;
  width: 100%;
  height: 70vh;
  overflow: hidden;
  border-radius: 12px;
  box-shadow: 0 8px 24px rgba(0,0,0,0.1);
}

.carousel-images {
  display: flex;
  transition: transform 0.5s ease-in-out;
}

.profile-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 12px;
  transition: transform 0.4s ease, box-shadow 0.3s ease;
}

.profile-image:hover {
  transform: scale(1.03);
  box-shadow: 0 6px 16px rgba(0, 0, 0, 0.15);
}

.about-right {
  flex: 1;
  text-align: left;
  padding: 20px;
  animation: fadeIn 1.4s ease-in;
}

h1 {
  font-size: 2.6rem;
  font-weight: 700;
  margin-bottom: 10px;
}

p {
  font-size: 1.1rem;
  margin-bottom: 12px;
  color: #444;
}

.quote {
  margin-top: 40px;
  font-style: italic;
  color: #555;
  border-left: 4px solid #4caf50;
  padding-left: 20px;
  background-color: #f9f9f9;
  border-radius: 8px;
}

.edit-button {
  margin-top: 20px;
  background-color: #4caf50;
  color: white;
  border: none;
  padding: 12px 24px;
  font-size: 1rem;
  font-weight: 500;
  border-radius: 6px;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.2s ease;
}

.edit-button:hover {
  background-color: #4241b6;
  transform: translateY(-2px);
}

/* Modal Styles */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
  animation: fadeIn 0.3s ease-out;
}

.modal {
  background: #fff;
  padding: 24px;
  border-radius: 12px;
  box-shadow: 0 6px 16px rgba(0, 0, 0, 0.2);
  width: 90%;
  max-width: 500px;
}

.modal h2 {
  margin-top: 0;
  font-size: 1.6rem;
  color: #333;
}

label {
  display: block;
  margin-bottom: 15px;
  font-size: 1rem;
  color: #555;
}

input,
textarea {
  width: 100%;
  padding: 10px;
  margin-top: 5px;
  border: 1px solid #ccc;
  border-radius: 6px;
  font-size: 1rem;
}

textarea {
  resize: none;
}

.modal-actions {
  display: flex;
  justify-content: flex-end;
  gap: 10px;
  margin-top: 20px;
}

.save-button {
  background-color: #4caf50;
  color: white;
  border: none;
  padding: 10px 24px;
  font-size: 1rem;
  border-radius: 6px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.save-button:hover {
  background-color: #43a047;
}

.cancel-button {
  background-color: #f44336;
  color: white;
  border: none;
  padding: 10px 24px;
  font-size: 1rem;
  border-radius: 6px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.cancel-button:hover {
  background-color: #d32f2f;
}

</style>