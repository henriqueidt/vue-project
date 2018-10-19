<template>
  <div class="third-component">
    <ul>
      <li v-for="language in languages" :key="language.id">
      <input type="checkbox" :id="language.name" name="babaga" value="language.name" v-on:click="language.show = !language.show"><label v-bind:for="language.name">{{ language.name }}</label>
      <h3 v-show="language.show">{{ language.speciality }}</h3>
      </li>
    </ul>
    <input type="text" v-model="inputLanguage" placeholder="other language" value=""/>
    <input type="button" value="Add" v-on:click="newLanguage()"/>
    <select name="tongues" multiple v-model="selectedTongues">
      <option v-for="tongue in tongues" :key="tongue.id">
      {{ tongue.name }}
      </option>
    </select>
  </div>
</template>

<script type = "text/javascript" >

export default {
  data: () => {
    return {
      languages: [
        { name: 'html', speciality: 'knows html', show: false},
        { name: 'css', speciality: 'knows css', show: false},
        { name: 'javascript', speciality: 'knows js', show: false},
      ],
      tongues: [
        { name: 'Portuguese', speciality: 'fala portugues', show: false},
        { name: 'English', speciality: 'speaks english', show: false},
        { name: 'Espanhol', speciality: 'hablas espanhol', show: false},
      ],
      inputLanguage: '',
      selectedTongues: [],
    }
  },
  methods: {
    newLanguage: function() {
      var languageObject = {};
      languageObject.name = this.inputLanguage;
      languageObject.speciality = `knows ${languageObject.name}`;
      languageObject.show = false;
      this.languages.push(languageObject)
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
  ul {
    list-style: none;
  }
</style>
