<template>
  <div class="second-component">
    <input type="text" id="city" v-model="city" placeholder="city"/>
    <input type="text" id="state" v-model="state" placeholder="state"/>
    <input type="text" v-model="cep" placeholder="cep"/>
    <input type="button" value="Check CEP" v-on:click="checkCep()"/>
  </div>
</template>

<script type = "text/javascript" >
import $ from 'jquery'

export default {
  props: {
    errors: {
      type: Array
    }
  },
  data: () => {
    return {
      city: '',
      state: '',
      cep: '',
      }
  },
  updated() {
    var cepLen = this.cep.length;
    var regexCityState = /^[a-zA-Z ]+$/;
    if(this.city.length > 50 || !this.city.match(regexCityState)) {
      if((this.errors.indexOf("Invalid city") == -1) && this.city.length != 0) {
        this.errors.push("Invalid city")
      }
    } else if (this.errors.indexOf("Invalid city") != -1) {
      this.errors.splice(this.errors.indexOf("Invalid city"),1)
    }
    if(this.state.length > 50 || !this.state.match(regexCityState)) {
      if((this.errors.indexOf("Invalid state") == -1) && this.state.length != 0) {
        this.errors.push("Invalid state")
      }
    } else if (this.errors.indexOf("Invalid state") != -1) {
      this.errors.splice(this.errors.indexOf("Invalid state"),1)
    }
    if(cepLen == 5) {
      this.cep += '-';
    }
  },
  methods: {
    checkCep: function() {
      var self = this;
      self.naoLocalizado = false;

      $.getJSON("https://viacep.com.br/ws/" + this.cep + "/json/", function(endereco){
          if(endereco.erro){
            alert("Cep nao encontrado!")
            self.naoLocalizado = true;
            return;
          }
          self.endereco = endereco;
          console.log(endereco)
          $('#city').val(endereco.localidade);
          $('#state').val(endereco.uf)
        });
    }
  }
};
</script>
<style>
  .second-component {
    display: flex;
    flex-direction: column;
    width: 500px;
  }
</style>
