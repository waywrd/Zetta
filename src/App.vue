<script setup>
import { ref } from 'vue';
import DataTable from './components/Table/DataTable.vue'
import Form from './components/Form/Form.vue'

const tableData = ref([])

function addTableRow(payload) {
  tableData.value.push(payload)
}
</script>

<template>
  <div>
    <div class='container'>
      <img src="./assets/zetta.png" alt="">
      <h1>Contact Form</h1>
      <Form @updateTableValue="addTableRow" />
    </div>
    <DataTable v-if='tableData.length' :tableData="tableData" />
    <div v-else>No data</div>
  </div>
</template>

<style scoped >
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
