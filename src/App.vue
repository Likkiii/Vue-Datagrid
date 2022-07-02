<template>
  <div class="navbar">
    <h2>Vue Datagrid</h2>
  </div>
  <div class="container">
    <div class="distinctRecords">
      <input
        type="text"
        class="searchBar"
        placeholder="Enter value..."
        v-model="searchText"
      />
      <div>
        <input
          type="checkbox"
          id="selectAll"
          @click="selectAll"
          v-model="allSelected"
        />
        <label for="selectAll">Select All</label>
      </div>
      <div v-for="(data, index) in filteredResources" :key="index">
        <input
          type="checkbox"
          :id="data"
          :value="data"
          v-model="selected"
          @click="select"
        />
        <label :for="data">{{ data }}</label>
      </div>
      <button class="filterBtn" @click="filterData">Apply</button>
      <!-- Cancel button to close the panel -->
    </div>
    <div class="grid">
      <template v-for="(data, index) in filterData" :key="index">
        <v-grid :source="data" :columns="columns" filter="true"></v-grid>
      </template>
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
      Data: Data,
      copyData: Data,
      searchText: "",
      picked: "first_name",
      selected: [],
      allSelected: true,
      columns: [
        {
          name: "ID",
          prop: "id",
          columnType: "number",
          sortable: true,
          columnProperties: ({ prop, model, data, column }) => {
            return {
              style: {
                color: "aliceblue",
                fontWeight: "bold",
                backgroundColor: "blue",
              },
            };
          },
        },
        {
          name: "Name",
          prop: "first_name",
          columnType: "string",
          sortable: true,
          columnProperties: ({ prop, model, data, column }) => {
            return {
              style: {
                color: "aliceblue",
                fontWeight: "bold",
                backgroundColor: "blue",
              },
            };
          },
        },
        {
          name: "Email",
          prop: "email",
          columnType: "email",
          size: 250,
          sortable: true,
          columnProperties: ({ prop, model, data, column }) => {
            return {
              style: {
                color: "aliceblue",
                fontWeight: "bold",
                backgroundColor: "blue",
              },
            };
          },
        },
        {
          name: "Phone",
          prop: "phone",
          columnType: "number",
          sortable: true,
          columnProperties: ({ prop, model, data, column }) => {
            return {
              style: {
                color: "aliceblue",
                fontWeight: "bold",
                backgroundColor: "blue",
              },
            };
          },
        },
        {
          name: "Gender",
          prop: "gender",
          columnType: "string",
          sortable: true,
          columnProperties: ({ prop, model, data, column }) => {
            return {
              style: {
                color: "aliceblue",
                fontWeight: "bold",
                backgroundColor: "blue",
              },
            };
          },
        },
        {
          name: "IP Address",
          prop: "ip_address",
          size: 200,
          columnType: "number",
          sortable: true,
          columnProperties: ({ prop, model, data, column }) => {
            return {
              style: {
                color: "aliceblue",
                fontWeight: "bold",
                backgroundColor: "blue",
              },
            };
          },
        },
      ],
    };
  },
  mounted() {
    this.distinctData();
  },
  computed: {
    filteredResources() {
      if (this.searchText) {
        return this.copyData
          .filter((item) =>
            item[this.picked]
              .toLowerCase()
              .includes(this.searchText.toLowerCase())
          )
          .map((item) => item[this.picked]);
      } else {
        return this.copyData.map((item) => item[this.picked]);
      }
    },
    filterData() {
      this.data = [];
      let details = this.Data.filter((data) =>
        this.selected.includes(data[this.picked])
      );
      this.data.push(details);
      return this.data;
    },
    selectAll() {
      this.selected = [];
      if (!this.allSelected) {
        for (let key in this.copyData) {
          var obj = this.copyData[key];
          this.selected.push(obj[this.picked]);
        }
      }
    },
  },
  methods: {
    distinctData() {
      this.selected = [
        ...new Set(this.copyData.map((item) => item[this.picked])),
      ];
    },
    select() {
      this.allSelected = false;
    },
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
  width: auto;
  overflow: auto;
  background: white;
}
.searchBar {
  border: black 2px solid;
  padding: 0.15rem 0.5rem;
}
.distinctRecords {
  background: rgb(152, 152, 152);
  height: 80%;
  overflow: auto;
}
.distinctRecords input {
  margin: 5px;
}
</style>
