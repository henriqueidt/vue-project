<template>
  <div class="fourth-component">
  <textarea  class="description" cols="30"  rows="10" v-model="description" placeholder="description"/>
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
      description: '',
      }
  },
  updated() {
    var bad_words=new Array("death","kill","murder","txai","bitch","fuck");
    var flag = false
    if(this.description.length > 200) {
      if((this.errors.indexOf("Invalid description") == -1) && this.description.length != 0) {
        this.errors.push("Invalid description")
      }
    } else if(this.errors.indexOf("Invalid description") != -1) {
      this.errors.splice(this.errors.indexOf("Invalid description"),1)
    }
    for(var i = 0; i < bad_words.length; i++) {
      var badWord = bad_words[i];
      if(this.description.toLowerCase().indexOf(badWord.toString()) != -1){
          flag = true
        if(this.errors.indexOf("Bad language") == -1) {
        this.errors.push("Bad language")
        }
      }
      }
      if((this.errors.indexOf("Bad language") != -1) && flag == false) {
        this.errors.splice(this.errors.indexOf("Bad language"),1)
      }
}
};
</script>
<style>
  .fourth-component {
    display: flex;
    flex-direction: column;
    width: 500px;
  }
</style>
