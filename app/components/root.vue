<template>
  <div>
    <submit></submit>
  </div>
</template>

<script>
module.exports = {
  name: 'root',
  props: {
  },
  components: {
    'submit': httpVueLoader('./submit.vue')
  },
  data: () => {
    return {
      
    }
  }
}
</script>


<style scoped>
*{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
</style>
