<template>
  <div
    v-click-outside="close"
    @click="toggle"
  >  
    <label 
      :for="id"
      class="base-input__lable"
    >
      {{ lable }}
    </label>
    <input
      :id="id"
      class="base-input"
      :value="value"
    />

    <div
      :id="id"
      v-if="opened"
    >
      <ul
        v-if="arr"
      >
        <li
          v-for="index in arr"
          :key="index"
          @click="onClick"
        >
          {{ index }}
        </li>
      </ul>
      <div
        v-else
      >
        Ничего не найдено
      </div>
    </div>
  </div>
</template>

<script>
import ClickOutside from "vue-click-outside";

export default {
  name: 'BaseDropdown',
  props: {
    id: {
      type: String,
      require
    },
    lable: {
      type: String,
      default: ''
    },
  },
  data() {
    return {
      opened: false,
      arr: [1,2,3,4,5],
      value: '',
    }
  },
  mounted() {
    if(this.arr) {
      this.value = this.arr[0]
    }
  },
  methods: {
    toggle() {
      this.opened = !this.opened
    },
    close() {
      this.opened = false
    },
    onClick(select) {
      this.value = select.target.textContent.trim()
    }
  },
  directives: {
    ClickOutside,
  },
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