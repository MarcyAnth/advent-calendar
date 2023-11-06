<template>
    <div>
        <img class="" v-bind:src="santaSlay">
    </div>
</template>

<script>

export default {
    name: 'SantaSlay',
  data() {
    return {
        santaSlay: require("../assets/santa.svg")
    };
  },

  computed: {

  },

  methods: {

  },

}
</script>