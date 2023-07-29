<script setup>
const props = defineProps({ tableData: [] })

function openDialog() {
    let dialog = document.getElementById('modal')
    dialog.showModal()
}
function closeDialog() {
    let dialog = document.getElementById('modal')
    dialog.close()
}


</script>
<template>
    <div>
        <button class='export-button' @click='openDialog()'>Export</button>
        <dialog id='modal'>
            <div>
                <span @click='closeDialog()' class='modal-close'>X</span>
                <pre>{{ JSON.stringify(tableData, null, 2) }}</pre>
            </div>
        </dialog>

    </div>
</template>
<style scoped>
.modal-close {
    position: absolute;
    top: 10px;
    right: 15px;
    cursor: pointer;
}
.export-button {
    background-color: #0E6DAA;
    color: white;
    margin-top: 30px;
    margin-bottom: 30px;
    text-transform: uppercase;
    font-weight: bold;
}
.export-button:hover {
    background-color: #065282;
    ;
}
</style>