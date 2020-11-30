<template>
  <div class="home">
    <router-link :to="{ name: 'create' }" class="button is-success my-5 mx-5">Create</router-link>
    <FAQList/>
  </div>
</template>

<script>
import FAQList from '../components/FAQList';

export default {
  components: {
    FAQList,
  },
};
</script>
