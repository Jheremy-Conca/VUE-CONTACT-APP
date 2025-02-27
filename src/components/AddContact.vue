<template>
  <div class="container mt-4">
    <div class="row justify-content-center">
      <div class="col-md-6">
        <div class="card shadow-lg p-4 rounded bg-dark text-light">
          <h2 class="text-center text-primary mb-4">Add New Contact</h2>
          <form @submit.prevent="saveContact">
            <div class="form-group mb-3">
              <input
                type="text"
                v-model="contact.name"
                class="form-control custom-input"
                placeholder="Enter Name"
              />
            </div>
            <div class="form-group mb-3">
              <input
                type="email"
                v-model="contact.email"
                class="form-control custom-input"
                placeholder="Enter Email"
              />
            </div>
            <div class="form-group mb-3">
              <input
                type="text"
                v-model="contact.phone"
                class="form-control custom-input"
                placeholder="Enter Phone"
              />
            </div>
            <div class="form-group mb-4">
              <input
                type="text"
                v-model="contact.designation"
                class="form-control custom-input"
                placeholder="Enter Designation"
              />
            </div>
            <button type="submit" class="btn btn-primary w-100">Submit</button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import axios from 'axios';
import { useToast } from 'vue-toastification';

const contact = ref({
  name: '',
  email: '',
  phone: '',
  designation: ''
});

const toast = useToast();

const saveContact = async () => {
  if (!contact.value.name || !contact.value.email || !contact.value.phone || !contact.value.designation) {
    toast.error("All fields are required!");
    return;
  }
  
  try {
    const url = "https://api-rest-nodejs-mongodb-contacts.onrender.com/api/contacts";
    const response = await axios.post(url, contact.value);
    
    if (response.status === 201) {
      toast.success('Contact Added Successfully');
      contact.value = { name: '', email: '', phone: '', designation: '' };
    }
  } catch (error) {
    console.error(error);
    toast.error("An error occurred while saving the contact.");
  }
};
</script>

<style scoped>
.card {
  border-radius: 15px;
  border: none;
}

.custom-input {
  background-color: #333;
  color: white;
  border: 1px solid #555;
  border-radius: 5px;
  transition: all 0.3s ease-in-out;
}

.custom-input:focus {
  border-color: #0d6efd;
  box-shadow: 0 0 10px rgba(13, 110, 253, 0.5);
}

.btn {
  font-size: 1.1rem;
  font-weight: bold;
  transition: 0.3s ease-in-out;
}

.btn:hover {
  transform: scale(1.05);
}
.custom-input::placeholder {
  color: rgb(192, 192, 192);
  opacity: 1; /* Asegura que el color se aplique completamente */
}

</style>
