<template>
  <div class="fifth-component">
    <input type="text" v-model="cpf" placeholder="cpf"/>
  </div>
</template>

<script type = "text/javascript" >

export default {
  props: {
    errors: {
      type: Array
    }
  },
  data: () => {
    return {
      cpf: '',
      }
  },
  updated() {
function testCPF(strCPF) {
  var sum, i;
  var rest;
  sum = 0;
  if (strCPF == "00000000000") return false;

  for (i=1; i<=9; i++) sum = sum + parseInt(strCPF.substring(i-1, i)) * (11 - i);
  rest = (sum * 10) % 11;

  if ((rest == 10) || (rest == 11))  rest = 0;
  if (rest != parseInt(strCPF.substring(9, 10)) ) return false;

  sum = 0;
  for (i = 1; i <= 10; i++) sum = sum + parseInt(strCPF.substring(i-1, i)) * (12 - i);
  rest = (sum * 10) % 11;

  if ((rest == 10) || (rest == 11))  rest = 0;
  if (rest != parseInt(strCPF.substring(10, 11) ) ) return false;
  return true;
}

    var regexCpf = /^[0-9]+$/;
    var cpfLen = this.cpf.length;
    if (cpfLen === 3 || cpfLen === 7) {
      this.cpf += '.';
    }
    if (cpfLen === 11) {
      this.cpf += '-';
    }
    if(this.cpf.length > 14) {
      if(this.errors.indexOf("Invalid cpf") == -1) {
        this.errors.push("Invalid cpf")
      }
    } else if (this.errors.indexOf("Invalid cpf") != -1) {
      this.errors.splice(this.errors.indexOf("Invalid cpf"),1)
    }
    var cleanCpf = this.cpf.replace(/[\.-]/g, "");
    if (!testCPF(cleanCpf) || !cleanCpf.match(regexCpf)) {
      if(this.errors.indexOf("Invalid number of cpf") == -1) {
        this.errors.push("Invalid number of cpf")
      }
    } else if (this.errors.indexOf("Invalid number of cpf") != -1) {
        this.errors.splice(this.errors.indexOf("Invalid number of cpf"),1)
      }
  }
}
</script>
<style>
  .fifth-component {
    display: flex;
    flex-direction: column;
    width: 500px;
  }
</style>
