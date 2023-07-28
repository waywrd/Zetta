
<script setup>

import Export from './Export.vue';
const props = defineProps({ tableData: [] })
const emit = defineEmits(['deleteRow'])

function deleteRow(index) {
    emit('deleteRow', index)
}

</script>
<template>
    <div class='table-container'>
        <table v-if='tableData.length'>
            <thead>
                <tr>
                    <th>Name</th>
                    <th>Surname</th>
                    <th>Email</th>
                    <th>Age</th>
                    <th>Favorite Color</th>
                    <th>Contact Preferences</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for='data, index in tableData' :key='index'>
                    <td>{{ data.name }}</td>
                    <td>{{ data.surname }}</td>
                    <td>{{ data.email }}</td>
                    <td>{{ data.age }}</td>
                    <td>{{ data.color }}</td>
                    <td>{{ data.contactPreference.join(' ,') }}</td>
                    <td class='__delete-button'>
                        <button @click='deleteRow(index)' class='delete-button'>Delete</button>
                    </td>

                </tr>
            </tbody>
        </table>
        <div class='empty-table' v-else>No data</div>
        <Export v-if="tableData.length" :tableData="tableData" :style="{ ' margin-top': '20px' }" />

    </div>
</template>
<style scoped lang='scss'>
.table-container {
    overflow: auto;

    @media screen and (max-width: 450px) {
        max-width: 400px;
    }
}

table {
    margin-top: 100px;
    border-spacing: 0;
    text-align: left;
    overflow: auto;
}

table .table-row,
td,
th {
    border: 1px solid black;
}

th,
td {
    text-align: left;
    padding: 10px 15px 5px 15px;
    background-color: whitesmoke;

    &.__delete-button {
        border: none;
        background-color: white;
    }
}

th {
    font-weight: bold;
    font-size: 19px;
}

.delete-button {
    background-color: red;
    color: white;
    font-size: 16px;
    font-weight: 500;
    padding: 15px 25px 15px 25px;
}

.export-button {
    color: red;
    margin-top: 100px;
}

.empty-table {
    display: flex;
    justify-content: space-around;
    align-items: center;
    height: 200px;
    flex-grow: 1;
    background-color: whitesmoke;
    font-size: 22px;
    width: 400px;
    font-weight: bold;
    margin-top: 28px;
    border-radius: 12px;
}
</style>