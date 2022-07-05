<template>
  <div class="navbar">
    <h2>Vue Datagrid</h2>
  </div>
  <div class="container">
    <div class="distinctRecords">
      <select id="select" v-model="picked">
        <option disabled value="">Select a property...</option>
        <option value="id">ID</option>
        <option value="first_name">Name</option>
        <option value="email">Email</option>
        <option value="phone">Phone</option>
        <option value="gender">Gender</option>
        <option value="ip_address">IP Address</option>
      </select>
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
        <v-grid
          :source="data"
          :columns="columns"
          filter="true"
          resize="true"
          exporting="true"
        ></v-grid>
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
          pin: "colPinStart",
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
        let details = this.copyData
          .filter((item) =>
            item[this.picked]
              .toLowerCase()
              .includes(this.searchText.toLowerCase())
          )
          .map((item) => item[this.picked]);
        this.selected = details;
        return details;
      } else {
        let dataDetails = this.copyData.map((item) => item[this.picked]);
        this.selected = dataDetails;
        return dataDetails;
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
  background: aliceblue;
}
.searchBar {
  border: black 2px solid;
  padding: 0.15rem 0.5rem;
  background: aliceblue;
}
.distinctRecords {
  display: flex;
  flex-direction: column;
  background: rgb(152, 152, 152);
  height: 80%;
  overflow: auto;
}
.distinctRecords input {
  margin: 5px;
}
#select {
  border: black 2px solid;
  background: aliceblue;
  padding: 0.15rem 0.5rem;
  margin: 5px 5px 0 5px;
}
.filterBtn {
  padding: 10px 20px;
  border-radius: 12px;
  border: none;
  color: antiquewhite;
  background: #6e29dc;
  font-weight: 600;
  cursor: pointer;
  box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
  margin-top: 0.5rem;
}
.filterBtn:hover {
  opacity: 0.9;
  box-shadow: rgba(0, 0, 0, 0.16) 0px 1px 4px;
  background: #5d1eca;
}
</style>
