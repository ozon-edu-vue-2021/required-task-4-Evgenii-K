<template>
    <div class="form__item">
        <div 
          class="form__passport-russian"
        >
        <base-input
          type="number"
          lable="Серия паспорта"
          id="passport_series_russian"
          v-model="passport.series"
          v-mask="'####'"
          @input="update"
        />      
        <base-input
          type="number"
          lable="Номер паспорта"
          id="passport_number_russian"
          v-model="passport.number"
          v-mask="'######'"
          @input="update"
        />      
        <base-input
          type="date"
          lable="Дата выдачи"
          id="date_of_issue"
          v-model="passport.date"
          @input="update"
        />
      </div>
    </div>
</template>

<script>
import BaseInput from './BaseInput'
import { VueMaskDirective } from "v-mask"

export default {
  data() {
    return {
      passport: {
        series: '',
        number: '',
        date: '',
      }
    };
  },
  components: {
    BaseInput,
  },
  methods: {
    update() {
      this.$emit('update', { russian: this.passport})
    }
  },
  directives: {
    mask: VueMaskDirective,
  }
};
</script>

<style scoped>

.form__item {
  display: grid;
  grid-gap: 20px;
}

.form__passport-russian {
  display: grid;
  grid-template-columns: 1fr 1fr 2fr;    
  grid-gap: 20px;
}
</style>
