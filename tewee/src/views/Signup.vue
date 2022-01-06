<template>
  <div class="canvas">
    <div class="form-wrapper">
      <h1 class="sm:text-8xl tracking-tighter text-7xl cursor-pointer">sign up</h1>
      <div id="signup-form" class="grid grid-cols-2 my-10">
        <input v-model="firstName" placeholder="first name" :class="{ fieldactive: firstName, errorfield: firstNameError }" class="grid-field" type="text">
        <input v-model="lastName" placeholder="last name" :class="{ fieldactive: lastName, errorfield: lastNameError }" class="grid-field border-l-0" type="text">
        <input v-model="email" placeholder="email address" :class="{ fieldactive: email, errorfield: emailError }" class="grid-field col-span-2" type="text">
        <input v-model="birthday" placeholder="birthday" class="grid-field pt-[-2px] max-h-[44px]" type="text" onfocus="(this.type='date')" onblur="(this.type='text')">
        <input v-model="gender" placeholder="gender" class="grid-field  border-l-0" type="text">
        <input v-model="userName" placeholder="username" :class="{ fieldactive: userName }" class="grid-field col-span-2" type="text">
        <input v-model="pwField" placeholder="password" :class="{ pwactive: pwField }" class="grid-field col-span-2" type="password">
        <input v-model="pwFieldConfirm" placeholder="confirm password" :class="{ pwactive: pwFieldConfirm }" class="grid-field col-span-2 border-b-[1px]" type="password">
      </div>
      <button @click="log()" class=" uppercase p-2 border-[1px] text-xl font-semibold tracking-wider">
        confirm
      </button>
    </div>
  </div>
</template>

<script lang="ts">
  import { defineComponent, reactive, toRefs } from 'vue';
  import * as EmailValidator from 'email-validator'; 

  export default defineComponent({
    name: 'Signup',
    components: {},
    setup() {
      let form = reactive({
        firstName: '',
        lastName: '',
        email: '',
        birthday: '',
        gender: '',
        userName: '',
        pwField: '',
        pwFieldConfirm: ''
      });

      let errorObj = reactive({
        firstNameError: false,
        lastNameError: false,
        emailError: false,
        birthdayError: false,
        genderError: false,
        userNameError: false,
        pwFieldError: false,
        pwFieldConfirmError: false
      });
    
      const log = () => {
        if (!form.firstName) {
          errorObj.firstNameError = true;
        }

        if (!form.lastName) {
          errorObj.lastNameError = true;
        }

        if (!EmailValidator.validate(form.email)) {
          errorObj.emailError = true;
        }

        let formDate = form.birthday.split('-');
        let today = new Date;
        let nowDays = today.toString().split(" ");
        console.log(formDate, nowDays);
        console.log(form.birthday);

        console.log(form);
        console.log(EmailValidator.validate(form.email));
        console.log(errorObj);
      }

      return { log , ...toRefs(form), ...toRefs(errorObj) };
    },
  });
</script>

<style scoped>
  h1, button {
    font-family: 'Playfair Display', serif;
  }

  .grid-field {
    padding-top: 11px;
    font-family: 'Montserrat', sans-serif;
    background-color: transparent;
  }

  /* .grid-field:focus {
    border-bottom: 1px !important;
  } */

  .pwactive {
    font-weight: 900;
    letter-spacing: 3px;
  }

  .fieldactive {
    text-transform: none;
  }

  .errorfield {
    height: 44px;
    border-bottom: solid;
  }

  .grid-field:focus::placeholder {
  color: transparent;
  }

  .grid-field::placeholder {
    color: black;
  }

  input[type="date"]::-webkit-inner-spin-button,
  input[type="date"]::-webkit-calendar-picker-indicator {
    display: none;
    -webkit-appearance: none;
  }
</style>