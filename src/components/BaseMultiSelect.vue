<template>
  <base-dropdown
    @close="blurHandler"
  >
    <template slot="drop-down-toggle">
      <div
        @click="clickOnInput"
      >
        <base-input
          :id="propName"
          :lable="lable"
          type="text"
          v-model="value"
        />
      </div>

    </template>

    <template 
      slot="drop-down-content"
      v-if="itemsAfterFilter.length"
    >
      <div 
        v-for="(item) in itemsAfterFilter" 
        :key="item.id"
        @click="selectHandler(item)"
      >
        {{ item[propName] }}
      </div>
    </template>

    <template 
      slot="drop-down-content"
      v-else
    >
      <div>
        Ничего не найдено
      </div>
    </template>
  </base-dropdown>
</template>

<script>
import BaseDropdown from './BaseDropdown.vue'
import BaseInput from './BaseInput.vue'

export default {
  props: {
    items: {
      type: Array,
      default: () => ({})
    },
    propName: {
      type: String,
      default: 'name'
    },
    selected: {
      type: Object,
      default: () => ({})
    },
    lable: {
      type: String,
      dafault: ''
    }
  },
  data() {
    return {
      value: '',
      itemsAfterFilter: []
    }
  },
  watch: {
    value() {

      if(!this.items.length) return

      if (this.value === '') {
        this.itemsAfterFilter = this.items
      } else {
        this.itemsAfterFilter = this.items.filter(item => 
          item[this.propName].toLowerCase().includes(this.value.toLowerCase())
        )
      }
    }
  },
  mounted() {
    if(this.items) {
      this.value = this.selected[this.propName]
    }
  },
  methods: {
    selectHandler(item) {
      this.$emit('update', item)
      this.value = item[this.propName]
    },
    blurHandler() {
      const target = this.items.filter(item => item[this.propName].toLowerCase() === this.value.toLowerCase())
      if (!target.length) {
        this.value = this.selected[this.propName]
      } else {
        this.value = target[0][this.propName]
        this.$emit('update', target[0])
      }
    },
    clickOnInput() {
      this.value = ''
    }
  },
  components: { BaseDropdown, BaseInput },
}
</script>

<style>

</style>