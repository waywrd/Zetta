<script setup>
import { ref } from 'vue';
const error = defineProps({ checkboxError: {}, resetCheckboxes: false })
const emit = defineEmits(['changePreference'])


const contactOptions = ref(['Email', 'Phone', 'Call', 'SMS'])

function changePreference(value) {
    emit('changePreference', value)

}



</script>
<template>
    <label class='checkbox-label'>Contact Preferences</label>
    <div class='checkbox-container'>
        <label class='contact-label' v-for="( option, index ) in  contactOptions " :key="index">
            <input @change='changePreference(option)' type="checkbox" :value="option"
                :checked="resetCheckboxes ? false : null" />
            <span class="checkmark"></span>
            {{ option }}
        </label>
    </div>
    <div class='error-message' v-if="checkboxError.state">{{ checkboxError.text }}</div>
</template>
<style>
.checkbox-container {
    display: flex;
    justify-content: space-between;
}
.checkbox-label {
    align-self: flex-start;
    font-size: 13px;
    padding-bottom: 1px;
}
.contact-label {
    position: relative;
    cursor: pointer;
    font-size: 17px;
    padding-left: 25px;
}
input[type='checkbox'] {
    opacity: 0;
    position: absolute;
    cursor: pointer;
}
.contact-label input:checked~.checkmark {
    background-color: white;
}
.checkmark {
    position: absolute;
    top: 3px;
    left: 4px;
    height: 15px;
    width: 15px;
    border: 1px solid #555;
    color: black;
    border-radius: 3px;
}
.checkmark:after {
    content: "";
    position: absolute;
    display: none;
}
.contact-label input:checked~.checkmark:after {
    display: block;
}
.contact-label .checkmark:after {
    left: 3px;
    bottom: 1px;
    width: 7px;
    height: 14px;
    border: solid black;
    border-width: 0 2px 2px 0;
    transform: rotate(40deg);
}
.error-message {
    align-self: flex-start;
    color: red;
    font-size: 13px;
    padding-top: 1px;
}
</style>