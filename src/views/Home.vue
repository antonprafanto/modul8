<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Daftar User</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content>
      <div style="text-align: center; margin: 20px;">
        <ion-button @click="fetchUsers">AMBIL DATA</ion-button>
      </div>
      <div class="table-container">
        <table>
          <thead>
            <tr>
              <th>id</th>
              <th>Name</th>
              <th>E-mail</th>
              <th>Company</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="user in users" :key="user.id">
              <td>{{ user.id }}</td>
              <td>{{ user.name }}</td>
              <td>{{ user.email }}</td>
              <td>{{ user.company.name }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';

interface User {
  id: number;
  name: string;
  email: string;
  company: {
    name: string;
  };
}

const users = ref<User[]>([]);
import { getUsers } from '../services/EndPointAccess';

export default defineComponent({
  setup() {
    // const users = ref([]);

    const fetchUsers = async () => {
      try {
        users.value = await getUsers();
      } catch (error) {
        console.error('Failed to fetch users:', error);
      }
    };

    return {
      users,
      fetchUsers,
    };
  },
});
</script>

<style scoped>
.table-container {
  overflow-x: auto;
  margin: 20px;
}

table {
  width: 100%;
  border-collapse: collapse;
  margin: auto;
}

th, td {
  border: 1px solid #ab2828;
  padding: 8px;
  text-align: left;
}

th {
  background-color: #f50101;
  font-weight: bold;
}

tr:hover {
  background-color: #725555;
}
</style>
