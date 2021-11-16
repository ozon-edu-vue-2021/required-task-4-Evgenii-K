<template>

  <div class="form__item">
    <div class="form__passport-name">
      <base-input
        type="text"
        label="Фамилия на латинице"
        id="second_name_latin"
        v-model.trim="passport.secondName"
        @input="update"
        required
        :error="errors.secondName"
      />      
      <base-input
        type="text"
        label="Имя на латинице"
        id="first_name_latin"
        v-model.trim="passport.firstName"
        @input="update"
        required
        :error="errors.firstName"
      />  

      <span class="form__passport-span">
        Иностранцы заполняют латинскими буквами. Например, Ivanov Ivan
      </span>  
    </div>

    <div class="form__passport-about">
      <base-input
        type="number"
        label="Номер паспорта"
        id="passport_number_russian"
        v-model="passport.number"
        @input="update"
        required
      />  
      <base-multi-select
        label="Страна выдачи"
        :items="citizenships"
        :prop-name="propCitizenship"
        :selected="selectedCitizenship"
        @update="updateCitizenship"
        required
      />     
      <base-multi-select
        label="Тип паспорта"
        :items="passportTypes"
        :prop-name="propPassportType"
        :selected="selectedPassportTypes"
        @update="updatePassportType"
        readonly
      />     
    </div>

  </div>
</template>

<script>
import BaseInput from '../BaseComponents/BaseInput'
import BaseMultiSelect from '../BaseComponents/BaseMultiSelect';
import citizenships from '../../assets/data/citizenships.json'
import passportTypes from '../../assets/data/passport-types.json'

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
  props: {
    errors: {
      type: Object,
      default: () => ({})
    }
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
