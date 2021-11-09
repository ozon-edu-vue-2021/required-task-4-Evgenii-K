<template>
  <div class="form__item">

    <div
      class="form__passport-name"
    >
      <base-input
        type="text"
        lable="Фамилия на латинице"
        id="second_name_latin"
        v-model="passport.secondName"
        @input="update"
      />      
      <base-input
        type="text"
        lable="Имя на латинице"
        id="first_name_latin"
        v-model="passport.firstName"
        @input="update"
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
        v-model="passport.number"
        @input="update"
      />  
      <base-multi-select
        lable="Страна выдачи"
        :items="citizenships"
        :prop-name="propCitizenship"
        :selected="selectedCitizenship"
        @update="updateCitizenship"
      />     
      <base-multi-select
        lable="Тип паспорта"
        :items="passportTypes"
        :prop-name="propPassportType"
        :selected="selectedPassportTypes"
        @update="updatePassportType"
        :readonly="true"
      />     
    </div>

  </div>
</template>

<script>
import BaseInput from './BaseInput'
import BaseMultiSelect from './BaseMultiSelect';
import citizenships from '../assets/data/citizenships.json'
import passportTypes from '../assets/data/passport-types.json'

export default {
  data() {
    return {
      citizenships,
      passportTypes,
      selectedPassportTypes: {},
      selectedCitizenship: {},
      propPassportType: 'type',
      propCitizenship: 'nationality',
      passport: {
        secondName: '',
        firstName: '',
        number: '',
        type: '',
        citizenship: '',
      },
    };
  },
  created() {
    if(this.citizenships.length) {
      this.citizenships = this.citizenships.filter(country => country[this.propCitizenship] !== 'Russia')
    }
    if(this.passportTypes.length) {
      this.selectedPassportTypes = this.passportTypes[0]
      this.passport.type = this.selectedPassportTypes[this.propPassportType]
    }
  },
  components: {
    BaseInput,
    BaseMultiSelect,
  },
  methods: {
    updateCitizenship(item) {
      this.selectedCitizenship = item
      this.passport.citizenship = this.selectedCitizenship[this.propCitizenship]
      this.update()
    },
    updatePassportType(item) {
      this.selectedPassportTypes = item
      this.passport.type = this.selectedPassportTypes[this.propPassportType]
      this.update()
    },
    update() {
      this.$emit('update', { foreign: this.passport })
    }
  },
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
