<template>
  <div class='first-component'>
    <input type='text' v-model='name' placeholder='name'/>
    <input type='text' v-model='phone' placeholder='phone'/>
    <input type='text' v-model='email' placeholder='email'/>
    <input type='text' v-model='birth' placeholder='birth'/>
    <cpf :errors='errors'></cpf>
  </div>
</template>

<script type = 'text/javascript' >
  import cpf from './cpf'

  export default {
    components: {
      cpf
    },
    props: {
      errors: {
        type: Array
      }
    },
    data() {
      return {
        name: '',
        phone: '',
        email: '',
        birth: '',
        }
    },
    updated() {
      const regexName = /^[a-zA-Z ]+$/;
      const regexPhone = /^([1-9]{1}[1-9]{1})\s([8-9]{1}[0-9]{3,4})[\/\-]([0-9]{4})$/;
      const regexEmail = /^([a-z]{5,})[@]([a-z]{3,}[.])([a-z]{2,3})[.]{0,1}([a-z]{0,3})$/
      const regexBirth =/^([0-9]{2})[\/\-]([0-9]{2})[\/\-]([0-9]{4})$/;
      let dateParts = this.birth.split('/');
      let birthLen = this.birth.length;
      let phoneLen = this.phone.length;
      if (phoneLen === 2) {
        this.phone += ' ';
      }
      if (phoneLen === 8) {
        this.phone += '-';
      }
      if (!this.phone.match(regexPhone) || this.phone.length > 13) {
        if ((this.errors.indexOf('Invalid phone') == -1) && this.phone.length != 0) {
          this.errors.push('Invalid phone')
      }
      } else if (this.errors.indexOf('Invalid phone') != -1) {
          this.errors.splice(this.errors.indexOf('Invalid phone'), 1)
      }
      if (this.name.length > 50 || !this.name.match(regexName)) {
        if ((this.errors.indexOf('Invalid name') == -1) && this.name.length != 0) {
          this.errors.push('Invalid name')
        }
      } else if (this.errors.indexOf('Invalid name') != -1) {
          this.errors.splice(this.errors.indexOf('Invalid name'), 1)
        }
      if (!this.email.match(regexEmail)) {
        if ((this.errors.indexOf('Invalid email') == -1) && this.email.length != 0) {
        this.errors.push('Invalid email')
        }
      } else if (this.errors.indexOf('Invalid email') != -1) {
          this.errors.splice(this.errors.indexOf('Invalid email'), 1)
      }
      if (birthLen === 2 || birthLen === 5) {
        this.birth += '/';
      }
      if (!regexBirth.test(this.birth) || dateParts[2] > 2001) {
        if ((this.errors.indexOf('Invalid birth date') == -1) && this.birth.length != 0) {
          this.errors.push('Invalid birth date')
        }
      } else if (this.errors.indexOf('Invalid birth date') != -1) {
          this.errors.splice(this.errors.indexOf('Invalid birth date'), 1)
      }
    }
  };
</script>
<style>
  .first-component {
    display: flex;
    flex-direction: column;
    width: 500px;
  }
</style>
