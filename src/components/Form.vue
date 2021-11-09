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
          lable="Фамилия"
          id="second_name"
          v-model="formDate.secondName"
        />      
        <base-input
          type="text"
          lable="Имя"
          id="first_name"
          v-model="formDate.firstName"
        />      
        <base-input
          type="text"
          lable="Отчество"
          id="third_name"
        />
      </div>

      <div class="form__birthday">
        <base-input
          type="date"
          lable="Дата рождения"
          id="birthday"
        />      
      </div>

      <div class="form__email">
        <base-input
          type="email"
          lable="E-mail"
          id="email"
        />      
      </div>
    </div>

    <div class="form__item">
      <div class="form__item-header">Пол</div>
      <base-radio
        :items="gender"
        :picked="'male'"
        @picked="updateGender"
      />
    </div>

    <div class="form__item">
      <div class="form__item-header">Паспортные данные</div>
      <div class="form__birthday">
        <base-multi-select
          lable="Гражданство"
          :items="citizenships"
          prop-name="nationality"
          :selected="selectedСitizenships"
          @update="updateCitizenships"
        />
      </div>
      <form-russian-citizenship v-if="isRussian"/>
      <form-other-citizenship v-else/>
    </div>

    <div class="form__item">
      <div class="form__item-header">Меняли ли фамилию или имя?</div>
      <base-radio
        :items="changedName"
        :picked="'false'"
        @picked="updateChangedName"
      />
    </div>

    <div 
      v-show="pickedChangedName === 'true'"
      class="form__birthday"
    >
      <base-input
        type="text"
        lable="Фамилия"
        id="new_second_name"
        v-model="formDate.newSecondName"
      />      
      <base-input
        type="text"
        lable="Имя"
        id="new_first_name"
        v-model="formDate.newFirstName"
      />     
    </div>


    <div class="form__button">
      <base-button>Отправить</base-button>
    </div>

  </form>
</template>

<script>
import BaseInput from './BaseInput'
import BaseButton from './BaseButton'
import FormRussianCitizenship from './FormRussianCitizenship';
import FormOtherCitizenship from './FormOtherCitizenship';
import BaseMultiSelect from './BaseMultiSelect';
import citizenships from '../assets/data/citizenships.json'
import BaseRadio from './BaseRadio.vue';

export default {
  data() {
    return {
      citizenships,
      selectedСitizenships: {},
      formDate: {
        firstName: '',
        secondName: '',
      },
      gender: [
        {
          name: 'male',
          title: 'Мужской'
        }, {
          name: 'famale',
          title: 'Женский'
        },
      ],
      pickedGender: '',
      changedName: [
        {
          name: 'false',
          title: 'Нет'
        }, {
          name: 'true',
          title: 'Да'
        }
      ],
      pickedChangedName: '',
    };
  },
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
    }
  },
  methods: {
    updateCitizenships(item) {
      this.selectedСitizenships = item
    },
    onSubmit() {
      console.log(this.formDate);
    },
    updateGender(value) {
      this.pickedGender = value
    },
    updateChangedName(value) {
      this.pickedChangedName = value
    }
  },
  computed: {
    isRussian() {
      return this.selectedСitizenships.nationality === 'Russia'
    }
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
