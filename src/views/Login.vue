<script>
import FormValidation from '../components/FormValidation.vue';
import Vee from '../components/Vee.vue';

export default {
  name: 'Login',
  components: {
    FormValidation,
    Vee,
  },
};
</script>

<template>
  <div id="login" class="container mt-5 mb-5" style="width: 900px">
    <FormValidation/>
    <Vee/>
  </div>
</template>

<style>
#login {
  display: flex;
  justify-content: space-between;
}

</style>
