<template>
  <div>
    <personalInfo :errors="errors"></personalInfo>
    <locationInfo :errors="errors"></locationInfo>
    <professionalInfo></professionalInfo>
    <description :errors="errors"></description>
    <p> {{ this.errors }}</p>
  </div>
</template>

<script>
import personalInfo from './components/personalInfo'
import locationInfo from './components/locationInfo'
import professionalInfo from './components/professionalInfo'
import description from './components/description'

export default {
  name: 'app',
  components: {
    personalInfo,
    locationInfo,
    professionalInfo,
    description
  },
  data() {
    return {
      errors: []
    }
  }
};
</script>

<style>
</style>
