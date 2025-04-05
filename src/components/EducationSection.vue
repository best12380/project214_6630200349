<template>
  <section id="education">
    <h2>Education</h2>
    <button @click="openForm()" class="add-button">Add Subject</button>
    <table>
      <thead>
        <tr>
          <th>Course Code</th>
          <th>Course Name</th>
          <th>Credits</th>
          <th>Grade</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(subject, index) in subjects" :key="index">
          <td>{{ subject.code }}</td>
          <td>{{ subject.name }}</td>
          <td>{{ subject.credits }}</td>
          <td>{{ subject.grade }}</td>
          <td>
            <button @click="editSubject(index)" class="edit-button">Edit</button>
            <button @click="deleteSubject(index)" class="delete-button">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>

    <!-- Form Modal -->
    <div v-if="showForm" class="modal-overlay">
      <div class="modal">
        <h2>{{ isEditing ? 'Edit Subject' : 'Add Subject' }}</h2>
        <form @submit.prevent="saveSubject">
          <label>
            Course Code:
            <input v-model="form.code" type="text" required />
          </label>
          <label>
            Course Name:
            <input v-model="form.name" type="text" required />
          </label>
          <label>
            Credits:
            <input v-model.number="form.credits" type="number" min="1" required />
          </label>
          <label>
            Grade:
            <input v-model="form.grade" type="text" required />
          </label>
          <div class="modal-actions">
            <button type="submit" class="save-button">Save</button>
            <button type="button" @click="closeForm" class="cancel-button">Cancel</button>
          </div>
        </form>
      </div>
    </div>
  </section>
</template>

<script>
import axios from "axios";

export default {
  name: "EducationSection",
  data() {
    return {
      subjects: [],
      showForm: false,
      isEditing: false,
      editIndex: null,
      form: {
        code: "",
        name: "",
        credits: null,
        grade: "",
      },
    };
  },
  mounted() {
    this.fetchSubjects();
  },
  methods: {
    async fetchSubjects() {
      const response = await axios.get("http://localhost:4000/subjects");
      this.subjects = response.data;
    },
    async saveSubject() {
      if (this.isEditing) {
        // Update existing subject
        await axios.put(`http://localhost:4000/subjects/${this.subjects[this.editIndex].id}`, this.form);
        this.subjects[this.editIndex] = { ...this.form };
      } else {
        // Add new subject
        const response = await axios.post("http://localhost:4000/subjects", this.form);
        this.subjects.push(response.data);
      }
      this.closeForm();
    },
    async deleteSubject(index) {
      const subjectId = this.subjects[index].id;
      await axios.delete(`http://localhost:4000/subjects/${subjectId}`);
      this.subjects.splice(index, 1);
    },
    openForm() {
      this.resetForm();
      this.showForm = true;
      this.isEditing = false;
    },
    closeForm() {
      this.showForm = false;
    },
    resetForm() {
      this.form = { code: "", name: "", credits: null, grade: "" };
      this.editIndex = null;
    },
    editSubject(index) {
      this.form = { ...this.subjects[index] };
      this.editIndex = index;
      this.isEditing = true;
      this.showForm = true;
    },
  },
};
</script>

<style scoped>
/* Table styles with enhanced design */
table {
  width: 100%;
  border-collapse: separate;
  border-spacing: 0;
  margin-top: 1.5rem;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
  border-radius: 8px;
  overflow: hidden;
}

th, td {
  padding: 0.8rem 1rem;
  text-align: left;
  border-bottom: 1px solid #eaeaea;
}

th {
  background-color: #f8f9fa;
  font-weight: 600;
  color: #444;
  position: relative;
}

th:after {
  content: "";
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 2px;
  background: linear-gradient(90deg, #6366f1, #8b5cf6);
  transform: scaleX(0);
  transition: transform 0.3s ease;
}

th:hover:after {
  transform: scaleX(1);
}

tr:last-child td {
  border-bottom: none;
}

tr:hover {
  background-color: #f8f9ff;
}

/* Button styles with animations */
button {
  padding: 0.6rem 1.2rem;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-weight: 500;
  transition: all 0.2s ease-in-out;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

button:before {
  margin-right: 0.5rem;
}

.add-button {
  background: linear-gradient(135deg, #4caf50, #2e7d32);
  color: white;
  margin-bottom: 1.2rem;
}

.add-button:before {
  content: "+";
  font-size: 1.2rem;
}

.edit-button {
  background: linear-gradient(135deg, #2196f3, #0d47a1);
  color: white;
  padding: 0.5rem 0.8rem;
}

.delete-button {
  background: linear-gradient(135deg, #f44336, #b71c1c);
  color: white;
  padding: 0.5rem 0.8rem;
  margin-left: 0.5rem;
}

button:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
}

button:active {
  transform: translateY(1px);
}

/* Modal styles with animations */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.6);
  backdrop-filter: blur(3px);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
  opacity: 0;
  animation: fadeIn 0.3s forwards;
}

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

.modal {
  background: #fff;
  padding: 2.5rem;
  border-radius: 12px;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
  width: 90%;
  max-width: 500px;
  transform: translateY(20px);
  animation: slideUp 0.3s forwards;
}

@keyframes slideUp {
  from { transform: translateY(20px); opacity: 0; }
  to { transform: translateY(0); opacity: 1; }
}

.modal h2 {
  margin-top: 0;
  margin-bottom: 1.5rem;
  color: #333;
  position: relative;
  padding-bottom: 0.5rem;
}

.modal h2:after {
  content: "";
  position: absolute;
  bottom: 0;
  left: 0;
  width: 60px;
  height: 3px;
  background: linear-gradient(90deg, #6366f1, #8b5cf6);
}

label {
  display: block;
  margin-bottom: 1.2rem;
  font-weight: 500;
  color: #444;
}

input {
  width: 100%;
  padding: 0.8rem;
  margin-top: 0.5rem;
  border: 1px solid #ddd;
  border-radius: 6px;
  transition: all 0.2s;
  font-size: 1rem;
}

input:focus {
  outline: none;
  border-color: #6366f1;
  box-shadow: 0 0 0 3px rgba(99, 102, 241, 0.2);
}

.modal-actions {
  display: flex;
  justify-content: flex-end;
  gap: 1rem;
  margin-top: 2rem;
}

.save-button {
  background: linear-gradient(135deg, #4caf50, #2e7d32);
  color: white;
}

.cancel-button {
  background: linear-gradient(135deg, #f44336, #b71c1c);
  color: white;
}
</style>