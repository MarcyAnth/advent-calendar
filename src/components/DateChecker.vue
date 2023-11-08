<template>
    <div></div>
  </template>
  
  <script>
  export default {
    name: 'DateChecker',
    data() {
      return {
        currentDate: new Date().toLocaleDateString(),
      };
    },
    methods: {
      checkForNewDay() {
        const currentDate = new Date().toLocaleDateString();
        console.log('clicked', currentDate)
        if (currentDate !== this.currentDate) {
          this.$emit('new-day');
          this.currentDate = currentDate;
        }
      },
    },
    mounted() {
      this.checkForNewDay();
      setInterval(this.checkForNewDay, 60000);
    },
  };
  </script>
  