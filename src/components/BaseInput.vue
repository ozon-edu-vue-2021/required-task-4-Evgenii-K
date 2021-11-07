<template>
  <div>  
    <label 
      :for="id"
      class="base-input__lable"
    >
      {{ lable }}
    </label>
    <input
      :id="id"
      class="base-input"
      :type="type"
    />
  </div>
</template>

<script>
export default {
  name: 'BaseInput',
  props: {
    id: {
      type: String,
      require
    },
    lable: {
      type: String,
      default: ''
    },
    type: {
      type: String,
      default: 'text'
    }
  }
}
</script>

<style scoped>
.base-input {
  background-color: #fff;
  width: 100%;
  border: 2px solid #dce0e6;
  border-radius: 5px;
  padding: 0px 10px;
  margin-top: 10px;
  font-size: 16px;
  height: 40px;
}

.base-input:focus-visible {
  border-color: #2459f6;
  outline: 0px solid #2459f6;
}

.base-input:active {
  border-color: #2459f6;
}

.base-input__lable {
  color: #8a99a9;
}



</style>