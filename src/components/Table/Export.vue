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
    <button @click='openDialog()'>Export</button>
    <dialog id='modal'>
        <div class='modal-content'>
            <span @click='closeDialog()' class='modal-close'>X</span>

            <pre>{{ JSON.stringify(tableData, null, 4) }}</pre>
        </div>
    </dialog>
</template>
<style scoped>
#data-dialog {
    position: relative
}
.modal-close {
    position: absolute;
    top: 10px;
    right: 15px;
    cursor: pointer;
}
</style>