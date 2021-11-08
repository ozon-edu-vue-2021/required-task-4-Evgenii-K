<template>
  <div class="form__item">

    <div
      class="form__passport-name"
    >
      <base-input
        type="text"
        lable="Фамилия на латинице"
        id="second_name_latin"
      />      
      <base-input
        type="text"
        lable="Имя на латинице"
        id="first_name_latin"
      />  

      <span
        class="form__passport-span"
      >
        Иностранцы заполняют латинскими буквами. Например, Ivanov Ivan
      </span>  
    </div>

    <div
      class="form__passport-about"
    >
      <base-input
        type="number"
        lable="Номер паспорта"
        id="passport_number_russian"
      />  
      <base-multi-select
        lable="Страна выдачи"
        :items="citizenships"
        prop-name="nationality"
        :selected="selectedСitizenships"
        @update="updateCitizenships"
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
import BaseMultiSelect from './BaseMultiSelect';
import citizenships from '../assets/data/citizenships.json'

export default {
  data() {
    return {
      citizenships,
      selectedСitizenships: {},
  };
  },
  created() {
    if(this.citizenships.length) {
      this.citizenships = this.citizenships.filter(country => country.nationality !== 'Russia')
    }
  },
  components: {
    BaseInput,
    BaseMultiSelect,
  },
  methods: {
    updateCitizenships(item) {
      this.selectedСitizenships = item
    },
  }
};
</script>

<style scoped>

.form__item {
  display: grid;
  grid-gap: 20px;
}

.form__passport-about {
  display: grid;
  grid-template-columns: 1fr 1fr 2fr;    
  grid-gap: 20px;
}

.form__passport-name {
  display: grid;
  grid-template-columns: 1fr 1fr;    
  grid-column-gap: 20px;
}

.form__passport-span {
  font-size: 12px;
  color: #8a99a9;
  padding-top: 8px;
}
</style>
