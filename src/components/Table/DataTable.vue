
<script setup>
import { ref } from 'vue';
import Export from './Export.vue';
const props = defineProps({ tableData: [] })
const emit = defineEmits(['deleteRow'])

const deleteIndex = ref()

function openDeleteModal(index) {
    let dialog = document.getElementById('delete-modal')
    deleteIndex.value = index;
    dialog.showModal()

}

function deleteRow(index) {
    let dialog = document.getElementById('delete-modal')
    dialog.close()
    emit('deleteRow', index)


}

function closeDeleteModal() {
    let dialog = document.getElementById('delete-modal')
    dialog.close()
}


</script>
<template>
    <div class='table-container'>
        <dialog id='delete-modal'>
            <div>
                <span @click='closeDeleteModal()' class='delete-modal-close'>X</span>
                <div class='delete-confirmation-container'>
                    <h3>Are you sure you want to delete current row?</h3>
                    <div class='delete-confirmation-container__buttons'>
                        <button class='delete-button' @click='deleteRow'>Delete</button>
                        <button @click='closeDeleteModal'>Cancel</button>
                    </div>
                </div>
            </div>
        </dialog>
        <table class='table' v-if='tableData.length'>
            <thead>
                <tr class='table-row'>
                    <th class='table-head'>Name</th>
                    <th class='table-head'>Surname</th>
                    <th class='table-head'>Email</th>
                    <th class='table-head'>Age</th>
                    <th class='table-head'>Favorite Color</th>
                    <th class='table-head'> Contact Preferences</th>
                </tr>
            </thead>
            <tbody>
                <tr class='table-row' v-for='data, index in tableData' :key='index'>
                    <td class='table-data'>{{ data.name }}</td>
                    <td class='table-data'>{{ data.surname }}</td>
                    <td class='table-data'>{{ data.email }}</td>
                    <td class='table-data'>{{ data.age }}</td>
                    <td class='table-data'>{{ data.color }}</td>
                    <td class='table-data'>{{ data.contactPreference.join(' ,') }}</td>
                    <td class='table-data__delete-button'>
                        <button @click='openDeleteModal(index)' class='delete-button'>Delete</button>
                    </td>

                </tr>
            </tbody>
        </table>
        <div class='empty-table' v-else>No data</div>

    </div>
    <Export v-if="tableData.length" :tableData="tableData" />
</template>
<style scoped >
.table-container {
    overflow: auto;
    @media screen and (max-width: 450px) {
        max-width: 400px;
    }
}
.table {
    margin-top: 100px;
    border-spacing: 0;
    text-align: left;
    overflow: auto;
}
.table .table-row,
.table-data,
.table-head {
    border: 1px solid black;
}
.table-head,
.table-data {
    text-align: left;
    padding: 10px 15px 5px 15px;
    background-color: whitesmoke;
}
td>.table-data__delete-button {
    border: none;
}
.table-head {
    font-weight: bold;
    font-size: 19px;
}
.delete-button {
    background-color: red;
    color: white;
    font-size: 16px;
    font-weight: bold;
    padding: 7px 22px 7px 22px;
    margin-left: 15px;
}
.delete-confirmation-container {
    display: flex;
    flex-direction: column;
}
.delete-confirmation-container__buttons {
    display: flex;
    justify-content: space-around;
}
.delete-modal {
    width: 100px;
}
.delete-modal-close {
    position: absolute;
    top: 5px;
    right: 5px;
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