<template>
  <div class="navbar">
    <h2>Vue Datagrid</h2>
  </div>
  <div class="container">
    <div class="grid">
      <v-grid :source="data" :columns="columns" filter="true"></v-grid>
    </div>
  </div>
</template>

<script>
import VGrid from "@revolist/vue3-datagrid";
import Data from "././assets/MOCK_DATA.json";

export default {
  name: "App",
  data() {
    return {
      data: Data,
      columns: [
        {
          name: "ID",
          prop: "id",
          columnType: "number",
        },
        {
          name: "Name",
          prop: "first_name",
          columnType: "string",
        },
        {
          name: "Email",
          prop: "email",
          columnType: "email",
          size: 250,
        },
        {
          name: "Phone",
          prop: "phone",
          columnType: "number",
        },
        {
          name: "Gender",
          prop: "gender",
          columnType: "string",
        },
        {
          name: "IP Address",
          prop: "ip_address",
          columnType: "number",
        },
      ],
    };
  },
  components: {
    VGrid,
  },
};
</script>

<style>
*,
*::before,
*::after,
html {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background: #2a2a2a;
  height: 100vh;
  overflow: hidden;
}
.navbar {
  width: 100%;
  background: #151515;
  padding: 20px 50px 20px 50px;
}
.navbar h2 {
  color: aliceblue;
  font-size: 1.9rem;
  font-weight: bold;
}
.container {
  margin-top: 2.5rem;
  height: 100%;
  width: 100%;
  display: flex;
  justify-content: center;
  column-gap: 6rem;
}
.grid {
  height: 80%;
  padding: 10px;
  background: #fff;
  width: auto;
  overflow: auto;
}
</style>
