<template>
  <div class="container mt-4">
    <div class="row justify-content-center">
      <div class="col-md-6">
        <div class="card shadow-lg p-4 rounded bg-dark text-light">
          <h2 class="text-center text-primary mb-4">Edit Contact</h2>
          <form @submit.prevent="updateContact">
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
            <button type="submit" class="btn btn-primary w-100">Update Contact</button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import axios from "axios";
import { useRouter, useRoute } from "vue-router";
import { useToast } from "vue-toastification";

const route = useRoute();
const router = useRouter();
const toast = useToast();

const contact = ref({
  name: "",
  email: "",
  phone: "",
  designation: "",
});

// Obtener contacto por ID
const getContactById = async () => {
  try {
    const url = `https://api-rest-nodejs-mongodb-contacts.onrender.com/api/contacts/${route.params.id}`;
    const response = await axios.get(url);
    contact.value = response.data;
  } catch (error) {
    console.log(error);
    toast.error("Error loading contact data");
  }
};

// Actualizar contacto
const updateContact = async () => {
  if (!contact.value.name || !contact.value.email || !contact.value.phone || !contact.value.designation) {
    toast.error("All fields are required!");
    return;
  }

  try {
    const url = `https://api-rest-nodejs-mongodb-contacts.onrender.com/api/contacts/${route.params.id}`;
    const response = await axios.put(url, contact.value);

    if (response.status === 200) {
      toast.success("Contact Updated Successfully");
      router.push({ name: "ContactList" });
    }
  } catch (error) {
    console.log(error);
    toast.error("Error updating contact");
  }
};

onMounted(() => {
  getContactById();
});
</script>

<style scoped>
/* Estilos para la tarjeta */
.card {
  border-radius: 15px;
  border: none;
}

/* Personalización de los inputs */
.custom-input {
  background-color: #333;
  color: white;
  border: 1px solid #555;
  border-radius: 5px;
  transition: all 0.3s ease-in-out;
}

/* Placeholder en blanco */
.custom-input::placeholder {
  color: white;
  opacity: 1;
}

.custom-input:focus {
  border-color: #0d6efd;
  box-shadow: 0 0 10px rgba(13, 110, 253, 0.5);
}

/* Botón estilizado */
.btn {
  font-size: 1.1rem;
  font-weight: bold;
  transition: 0.3s ease-in-out;
}

.btn:hover {
  transform: scale(1.05);
}
</style>
