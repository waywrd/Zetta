<script setup>
import { ref } from 'vue';
import Checkbox from './Checkbox.vue'

const emit = defineEmits(['updateTableValue'])

const errors = ref({
    emailError: {
        state: false,
        text: 'Please enter a valid email address'
    },

    ageError: {
        state: false,
        text: 'Please select  age under 120'
    },
    checkboxError: {
        state: false,
        text: 'Add at least one contact preference'
    }

})

const form = ref({
    name: '',
    surname: '',
    email: '',
    age: '',
    color: '',
    contactPreference: [],
});

function isValidEmail(email) {
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    const isValid = emailRegex.test(email);
    return isValid;
}



function isAgeValid(age) {
    if (age > 120) {
        return false
    }
    return true
}

function isValidContactPreference(preferences) {
    if (preferences.length) {
        errors.value.checkboxError.state = false
        return true
    }
    return false
}

function changePreference(payload) {
    console.log(payload)
    if (form.value.contactPreference.includes(payload)) {
        form.value.contactPreference = form.value.contactPreference.filter(p => p !== payload)
    }
    else {
        form.value.contactPreference.push(payload)

    }
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
            <div class='first-row'>
                <input class='form-input' placeholder='Name' v-model='form.name' id='name' type="text">
                <input class='form-input' placeholder='Surname' v-model='form.surname' type="text">
            </div>
            <div class='second-row'>
                <div class='email-field'>
                    <input class='form-input email-input' placeholder='Email address' v-model='form.email' type="text">
                    <div class='error-message' v-if='errors.emailError.state'>{{ errors.emailError.text }}</div>

                </div>
                <div class='age-container'>
                    <label class='label' for='age'>Age</label>
                    <select class='select' v-model="form.age">
                        <option value="" selected disabled>Select Age</option>
                        <option v-for='age in Array.from({ length: 108 }, (_, index) => 14 + index)'>{{ age }}</option>
                    </select>
                    <div class='error-message' v-if='errors.ageError.state'>{{ errors.ageError.text }}</div>

                </div>


            </div>
            <div class='third-row'>
                <label class='label favorite-color-label' for="favoriteColor">Favorite Color</label>
                <select class='select favorite-color-select' id='favoriteColor' v-model="form.color">
                    <option disabled value="">Select a color</option>
                    <option>Red</option>
                    <option>Green</option>
                    <option>Blue</option>
                    <option>White</option>
                    <option>Black</option>
                </select>
            </div>
            <div class='fourth-row'>
                <Checkbox @changePreference='changePreference' :checkboxError='errors.checkboxError' />
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

.first-row {
    display: flex;
    justify-content: space-between;
    padding-top: 10px;

    &__surname {
        margin-left: 20px;
    }
}

.second-row {
    display: flex;
    justify-content: flex-start;
    padding-top: 5px;
}

.third-row {
    display: flex;
    flex-direction: column;
    padding-top: 15px;
    width: 100%;
}

.fourth-row {
    display: flex;
    flex-direction: column;
    margin-top: 20px;
}

.form-input {
    font-size: 16px;
    height: 22px;
    padding: 10px 8px 7px 8px;
    border: 1px solid lightgray;
    border-radius: 5px;
    background-color: whitesmoke;
}

.age-container {
    display: flex;
    flex-direction: column;
    padding-left: 32px;
    padding-top: 8px;
    width: 130px;
}

.email-field {
    padding-top: 28px;
    flex-grow: 1;
}

.email-input {
    width: 92%;
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

.favorite-color-select {
    width: 100%
}

.favorite-color-label {
    align-self: flex-start;
}

.select {
    padding: 11px 7px 10px 3px;
    background-color: whitesmoke;
    border: 1px solid lightgray;
    border-radius: 5px;
    font-size: 16px;
    appearance: none;
}

.label {
    align-self: flex-start;
    font-size: 13px;
    padding-bottom: 1px;
}

.submit-button {
    margin-top: 30px;
    background-color: #88C562;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
    color: white;
}
</style>