<template>
    <div class="form__item">
        <div 
          class="form__passport-russian"
        >
        <base-input
          type="number"
          lable="Серия паспорта"
          id="passport_series_russian"
        />      
        <base-input
          type="number"
          lable="Номер паспорта"
          id="passport_number_russian"
        />      
        <base-input
          type="date"
          lable="Дата выдачи"
          id="date_of_issue"
        />
      </div>
    </div>
</template>

<script>
import BaseInput from './BaseInput'
export default {
  data() {
    return {};
  },
  components: {
    BaseInput,
  },
  methods: {},
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
