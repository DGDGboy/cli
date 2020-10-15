<script>
import FormValidation from '../components/FormValidation.vue';

export default {
  name: 'Login',
  components: {
    FormValidation,
  },
};
</script>

<template>
  <div id="login" class="container mt-5 mb-5" style="width: 500px">
    <FormValidation/>
  </div>
</template>
