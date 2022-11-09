<template>
  <div>
    <div v-if="error">
      <h2>Error: {{ error }}</h2>
    </div>
    <div v-else>
      <div v-if="loading">
        <h2>Loading data ....</h2>
      </div>
      <h1>Users</h1>
      <table class="styled-table">
        <thead>
          <tr>
            <th>Name</th>
            <th>UserName</th>
            <th>ZIP</th>
            <th>City</th>
            <th>Street</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in data" :key="index">
            <td>{{ item.name }}</td>
            <td>{{ item.username }}</td>
            <td>{{ item.address.zipcode }}</td>
            <td>{{ item.address.city }}</td>
            <td>{{ item.address.street }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import { useFetch } from '../composables/UseFetch.js';
export default {
  setup() {
    const { data, error, loading } = useFetch(
      'https://jsonplaceholder.typicode.com/users',
      {}
    );
    console.log(data.value);
    return {
      data,
      error,
      loading,
    };
  },
};
</script>

<style scoped>
.styled-table {
  border-collapse: collapse;
  margin: 25px 0;
  font-size: 0.9em;
  font-family: sans-serif;
  min-width: 400px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.15);
}
.styled-table thead tr {
  background-color: #009879;
  color: #ffffff;
  text-align: left;
}
.styled-table th,
.styled-table td {
  padding: 12px 15px;
  text-align: left;
}
styled-table tbody tr {
  border-bottom: 1px solid #dddddd;
}

.styled-table tbody tr:nth-of-type(even) {
  background-color: #f3f3f3;
}

.styled-table tbody tr:last-of-type {
  border-bottom: 2px solid #009879;
}
h1 {
  text-align: center;
}
</style>
