<template>
  <div class="mobileField">
    <label class="label">{{field_label}}</label>
    <input class="input" type="tel" :value="value" 
    @input="$emit('input', $event.target.value)" />
  </div>
</template>

<script>
module.exports = {
  name: 'mobilefield',
  props: [
    'field_label',
    'value'
  ],
  components: {
  }
}
</script>



<style scoped>

.mobileField {
  margin: 20px 0;
}

.label {
  display: block;
  margin: 5px 0;
  color: white;
  font-size: 1rem;
  font-size: 1.2rem;
  font-weight: 500;
}

.input {
  border: none;
  box-shadow: 0px 0px 3px black;
  border-radius: 4px;
  width: 100%;
  height: 25px;
  padding: 15px;
  font-weight: 600;
  font-size: 1rem;
}

.input:hover {
  box-shadow: 0px 0px 15px black;
}

</style>