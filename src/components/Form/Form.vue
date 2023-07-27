<script setup>
import { ref } from 'vue';

const emit = defineEmits(['updateTableValue'])

const errors = ref({
    emailError: {
        state: false,
        text: 'Please enter a valid email address'
    },
    checkboxError: {
        state: false,
        text: 'Add at least one contact preference'
    },
    ageError: {
        state: false,
        text: 'Please select an age under 120 years'
    }
})

const form = ref({
    name: '',
    surname: '',
    email: '',
    age: 22,
    color: '',
    contactPreference: ['Call'],
});
const contactOptions = ['Email', 'Phone', 'Call', 'SMS'];

function isValidEmail(email) {
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    const isValid = emailRegex.test(email);
    return isValid;
}

function isValidContactPreference(preferences) {
    if (preferences.length) {
        errors.value.checkboxError.state = false
        return true
    }
    return false
}

function isAgeValid(age) {
    if (age > 120) {
        return false
    }
    return true
}

function submitForm() {
    let isFormValid = true

    if (!isValidEmail(form.value.email)) {
        errors.value.emailError.state = true;
        isFormValid = false
    }
    if (!isValidContactPreference(form.value.contactPreference)) {
        errors.value.checkboxError.state = true;
        isFormValid = false
    }
    if (!isAgeValid(form.value.age)) {
        errors.value.ageError.state = true
        isFormValid = false

    }
    if (isFormValid) {
        let formDataDeepCopy = JSON.parse(JSON.stringify(form.value))
        emit('updateTableValue', formDataDeepCopy)
    }

}
</script>

<template>
    <form>
        <div class='form-row'>
            <div class='names-row'>
                <input placeholder='Name' v-model='form.name' id='name' type="text">
                <input placeholder='Surname' v-model='form.surname' class='names-row__surname' type="text">
            </div>
            <div class='names-row'>
                <input placeholder='Email address' v-model='form.email' id='email' type="text">
                <div class='error-message' v-if='errors.emailError.state'>{{ errors.emailError.text }}</div>
                <label>Age</label>
                <input v-model="form.age" id='age' type="number">
                <div class='error-message' v-if='errors.emailError.state'>{{ errors.ageError.text }}</div>
            </div>
            <label for="favoriteColor">Favorite Color</label>
            <select id='favoriteColor' v-model="form.color">
                <option disabled value="">Select a color</option>
                <option>Red</option>
                <option>Green</option>
                <option>Blue</option>
                <option>White</option>
                <option>Black</option>
            </select>
            <div> Contact Preferences</div>
            <div class='chechbox-container'>
                <label v-for="( option, index ) in  contactOptions " :key="index">
                    <input @change='isValidContactPreference(form.contactPreference)' type="checkbox" :value="option"
                        v-model="form.contactPreference" /> {{ option }}
                </label>
                <div class='error-message' v-if='errors.checkboxError.state'>{{ errors.checkboxError.text }}</div>

            </div>
            <button class='submit-button' @click.prevent='submitForm'>Submit</button>
        </div>
    </form>
</template>
<style scoped lang='scss'>
.form-row {
    display: flex;
    flex-direction: column;
    width: 400px;
    justify-content: space-around;
}

.names-row {
    display: flex;

    &__surname {
        margin-left: 20px;
    }
}

input {
    font-size: 16px;
    padding: 10px 8px 7px 8px;
    border: 1px solid lightgray;
    border-radius: 5px;
    background-color: whitesmoke;
}

input[type='number'] {
    max-width: 100px;
}

select {
    padding: 12px 7px 7px 3px;
    background-color: whitesmoke;
    border: 1px solid lightgray;
    border-radius: 5px;
}

.chechbox-container {
    display: flex;
    justify-content: space-around;
}

.error-message {
    align-self: flex-start;
    color: red;
    font-size: 13px;
    padding-top: 1px;
}

label {
    font-weight: bold;
    align-self: flex-start;
    padding-top: 10px;
    display: block;
}

.submit-button {
    margin-top: 45px;
    background-color: #88C562;
}
</style>