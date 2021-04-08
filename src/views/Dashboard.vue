<template>
  <div>
    <h1>Dashboard</h1>
    <v-data-table
      :headers="headers"
      :items="employees"
      :items-per-page="5"
      class="elavation-1"
      @click:row="selectRow"
    >
    </v-data-table>
    <v-snackbar v-model="snackbar"
      >You have selected {{ selectedEmployee.name }} ({{ selectedEmployee.title }})
      <v-btn color="pink" text @click="snackbar = false">Close</v-btn>
    </v-snackbar>
  </div>
</template>

<script>
import employeesData from '@/data/employees.json'

export default {
  name: "DashboardPage",
  methods: {
    selectRow(event) {
      this.snackbar = true;
      this.selectedEmployee.name = event.name;
      this.selectedEmployee.title = event.title;
    },
  },
  data() {
    return {
      selectedEmployee: {
          name: '', title: ''
      },
      snackbar: false,
      headers: [
        {
          text: "Employee Id",
          align: "left",
          sortable: true,
          value: "id",
        },
        { text: "Name", value: "name", sortable: true },
        { text: "Job Title", value: "title", sortable: true },
        { text: "Salary", value: "salary", sortable: true },
      ],
      employees: employeesData,
    };
  },
};
</script>

<style lang="scss" scoped></style>
