<template>
  <div class='fourth-component'>
    <textarea  class='description' cols='30'  rows='10' v-model='description' placeholder='description'/>
  </div>
</template>

<script type = 'text/javascript' >

  export default {
    props: {
      errors: {
        type: Array
      }
    },
    data() {
      return {
        description: '',
        bad_words: ['death','kill','murder','txai','bitch','fuck']
      }
    },
    updated() {
      let flag = false
      if (this.description.length > 200) {
        if ((this.errors.indexOf('Invalid description') == -1) && this.description.length != 0) {
          this.errors.push('Invalid description')
        }
      } else if (this.errors.indexOf('Invalid description') != -1) {
        this.errors.splice(this.errors.indexOf('Invalid description'), 1)
      }
      this.bad_words.forEach ((item) =>  {
        let badWord = item;
        if (this.description.toLowerCase().indexOf(badWord.toString()) != -1){
            flag = true
          if (this.errors.indexOf('Bad language') == -1) {
          this.errors.push('Bad language')
          }
        }
      });
      if ((this.errors.indexOf('Bad language') != -1) && flag == false) {
        this.errors.splice(this.errors.indexOf('Bad language'), 1)
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
