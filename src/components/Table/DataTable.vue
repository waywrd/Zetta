
<script setup>
import ExportButton from './ExportButton.vue';
const props = defineProps({ tableData: [] })

</script>
<template>
    <div class='table-container'>
        <table>
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
                <tr v-for='data in tableData'>
                    <td>{{ data.name }}</td>
                    <td>{{ data.surname }}</td>
                    <td>{{ data.email }}</td>
                    <td>{{ data.age }}</td>
                    <td>{{ data.color }}</td>
                    <td>{{ data.contactPreference.join(' ,') }}</td>
                    <td class='__delete-button'>
                        <button class='delete-button'>Delete</button>
                    </td>

                </tr>
            </tbody>
        </table>
        <ExportButton :tableData="tableData" class='export-button' />
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
    margin-top: 40px;
}
</style>