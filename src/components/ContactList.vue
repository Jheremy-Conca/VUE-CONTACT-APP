<template>
  <div class="container mt-4">
    <div class="text-center" v-if="loading">
      <ClipLoader color="#0d6efd" size="50px" />
    </div>
    <div v-else>
      <h2 class="text-light mb-3">Contact List</h2>
      
      <!-- Search Bar -->
      <input 
        type="text" 
        v-model="searchQuery" 
        class="form-control mb-3" 
        placeholder="Search by name..."
      />

      <div v-if="filteredContacts.length === 0" class="text-center text-light">
        No contacts found.
      </div>
      <table v-else class="table table-dark table-hover shadow rounded">
        <thead class="table-primary">
          <tr>
            <th>Name</th>
            <th>Email</th>
            <th>Contact No#</th>
            <th>Designation</th>
            <th>Action</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="contact in filteredContacts" :key="contact.id">
            <td>{{ contact.name }}</td>
            <td>{{ contact.email }}</td>
            <td>{{ contact.phone }}</td>
            <td>{{ contact.designation }}</td>
            <td>
              <router-link 
                :to="{ name: 'EditContact', params: { id: contact._id } }" 
                class="btn btn-primary btn-sm me-2"
              >Edit</router-link>
              <button 
                class="btn btn-danger btn-sm"
                @click="deleteContact(contact._id)"
              >Delete</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>
import axios from "axios";
import { ref, onMounted, computed } from "vue";
import ClipLoader from 'vue-spinner/src/ClipLoader.vue';
import { useToast } from "vue-toastification";

const contacts = ref([]);
const loading = ref(true);
const toast = useToast();
const searchQuery = ref("");
const apiURL = "https://api-rest-nodejs-mongodb-contacts.onrender.com/api/contacts";

const getContacts = async () => {
  try {
    const response = await axios.get(apiURL);
    contacts.value = response.data;
  } catch (error) {
    console.error(error);
  } finally {
    loading.value = false;
  }
};

const deleteContact = async (id) => {
  try {
    if (confirm("Are you sure you want to delete the contact?")) {
      const response = await axios.delete(`${apiURL}/${id}`);
      if (response.status === 200) {
        toast.success("Contact Deleted Successfully");
        getContacts();
      }
    }
  } catch (error) {
    console.error(error);
  }
};

const filteredContacts = computed(() => {
  return contacts.value.filter(contact => 
    contact.name.toLowerCase().includes(searchQuery.value.toLowerCase())
  );
});

onMounted(getContacts);
</script>

<style scoped>
.container {
  background: #212529;
  padding: 20px;
  border-radius: 10px;
}

.table {
  border-radius: 10px;
  overflow: hidden;
}

.table-hover tbody tr:hover {
  background-color: rgba(13, 110, 253, 0.2);
}

h2 {
  text-align: center;
  font-weight: bold;
}

.btn-sm {
  transition: 0.3s ease-in-out;
}

.btn-sm:hover {
  transform: scale(1.05);
}
</style>
