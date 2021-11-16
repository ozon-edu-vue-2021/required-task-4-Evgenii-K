<template>
  <form 
    class="form"
    @submit.prevent="onSubmit"
  >
    <div class="form__item">
      <div class="form__item-header">Личные данные</div>
      <div class="form__name-cyrillic">
        <base-input
          type="text"
          label="Фамилия"
          id="second_name"
          v-model.trim="formData.secondName"
          required
          :error="errors.secondName"
        />      
        <base-input
          type="text"
          label="Имя"
          id="first_name"
          v-model.trim="formData.firstName"
          required
          :error="errors.firstName"
        />      
        <base-input
          type="text"
          label="Отчество"
          id="third_name"
          v-model.trim="formData.thirdName"
          :error="errors.thirdName"
        />
      </div>

      <div class="form__birthday">
        <base-input
          type="date"
          label="Дата рождения"
          id="birthday"
          v-model="formData.birthday"
          required
          :max="todaysDay"
        />      
      </div>

      <div class="form__email">
        <base-input
          type="email"
          label="E-mail"
          id="email"
          v-model.trim="formData.email"
          required
          :error="errors.email"
        />      
      </div>
    </div>

    <div class="form__item">
      <div class="form__item-header">Пол</div>
      <base-radio
        :items="genderTitle"
        :picked="formData.gender"
        @picked="updateGender"
      />
    </div>

    <div class="form__item">
      <div class="form__item-header">Паспортные данные</div>
      <div class="form__birthday">
        <base-multi-select
          label="Гражданство"
          :items="citizenships"
          :prop-name="propCitizenship"
          :selected="selectedСitizenships"
          @update="updateCitizenships"
        />
      </div>
      <form-russian-citizenship 
        v-if="isRussian"
        @update="updatePassport"
        :errors="errors.russian"
      />
      <form-other-citizenship 
        v-else
        @update="updatePassport"
        :errors="errors.foreign"
      />
    </div>

    <div class="form__item">
      <div class="form__item-header">Меняли ли фамилию или имя?</div>
      <base-radio
        :items="previousNameTitle"
        :picked="previousName"
        @picked="updateName"
      />
    </div>

    <div 
      v-show="isPreviousName"
      class="form__birthday"
    >
      <base-input
        type="text"
        label="Фамилия"
        id="new_second_name"
        v-model.trim="formData.previous.secondName"
        :required="isPreviousName"
      />      
      <base-input
        type="text"
        label="Имя"
        id="new_first_name"
        v-model.trim="formData.previous.firstName"
        :required="isPreviousName"
      />     
    </div>


    <div class="form__button">
      <base-button type="submit">Отправить</base-button>
    </div>

  </form>
</template>

<script>
import BaseInput from '../BaseComponents/BaseInput'
import BaseButton from '../BaseComponents/BaseButton'
import FormRussianCitizenship from './FormRussianCitizenship';
import FormOtherCitizenship from './FormOtherCitizenship';
import BaseMultiSelect from '../BaseComponents/BaseMultiSelect';
import citizenships from '../../assets/data/citizenships.json'
import BaseRadio from '../BaseComponents/BaseRadio.vue';
import VuelidateMixin from '../../utils/VuelidateMixin.vue'
import TodaysDate from '../../utils/TodaysDate.vue'

export default {
  data() {
    return {
      citizenships,
      selectedСitizenships: {},
      propCitizenship: 'nationality',
      formData: {
        firstName: '',
        secondName: '',
        thirdName: '',
        birthday: '',
        email: '',
        gender: 'male',
        citizenship: '',
        previous: {
          firstName: '',
          secondName: '',
        }
      },
      passport: {
        russian: {
          series: '',
          number: '',
          date: '',
        },
        foreign: {
          secondName: '',
          firstName: '',
          number: '',
          type: '',
          citizenship: '',
        },
      },
      genderTitle: [
        {
          name: 'male',
          title: 'Мужской'
        }, {
          name: 'female',
          title: 'Женский'
        },
      ],
      previousName: 'false',
      previousNameTitle: [
        {
          name: 'false',
          title: 'Нет'
        }, {
          name: 'true',
          title: 'Да'
        }
      ],
    };
  },
  mixins: [ VuelidateMixin, TodaysDate ],
  components: {
    BaseInput,
    BaseButton,
    BaseMultiSelect,
    FormRussianCitizenship,
    FormOtherCitizenship,
    BaseRadio,
  },
  created() {
    if(this.citizenships.length) {
      this.selectedСitizenships = this.citizenships[0]
      this.formData.citizenship = this.selectedСitizenships[this.propCitizenship]
    }
  },
  methods: {
    updateCitizenships(item) {
      this.selectedСitizenships = item
      this.formData.citizenship = this.selectedСitizenships[this.propCitizenship]
    },
    onSubmit() {
      this.$v.$touch()

      if (!this.$v.$invalid) {
        const result = {...this.formData, passport: this.passport }
        console.log(JSON.stringify(result));  
      }
    },
    updateGender(value) {
      this.formData.pickedGender = value
    },
    updateName(value) {
      this.previousName = value
    },
    updatePassport(value) {
      this.passport =  {...this.passport, ...value}
    },

  },
  computed: {
    isRussian() {
      return this.selectedСitizenships.nationality === 'Russia'
    },
    isPreviousName() {
      return this.previousName === 'true'
    },
  },
};
</script>

<style scoped>
.form {
  display: grid;
  grid-gap: 20px;
  width: 800px;
}
.form__item {
  display: grid;
  grid-gap: 20px;
}
.form__item-header {
  font-size: 18px;
  font-weight: 500;
}
.form__name-cyrillic {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-gap: 20px;
}
.form__birthday {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 20px;
}
.form__email {
  display: grid;
  grid-template-columns: 1fr;
}
.form__button {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  margin-top: 30px;
}
</style>
