<script setup>
import { ref } from 'vue';
import DataTable from './components/Table/DataTable.vue'
import Form from './components/Form/Form.vue'
import Header from './components/Header.vue'

const tableData = ref([])

function addTableRow(payload) {
  tableData.value.push(payload)
}
function deleteRow(payload) {
  tableData.value.splice(payload, 1)
}

</script>

<template>
  <div class='container'>
    <Header />
    <Form @updateTableValue="addTableRow" />
    <DataTable @deleteRow='deleteRow' :tableData="tableData" />

  </div>
</template>

<style scoped >
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
