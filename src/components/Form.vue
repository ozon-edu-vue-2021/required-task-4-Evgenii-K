<template>
  <div class="form">
    <div class="form__item">
      <div class="form__item-header">Личные данные</div>
      <div 
        class="form__name-cyrillic"
      >
        <base-input
          type="text"
          lable="Фамилия"
          id="second_name"
        />      
        <base-input
          type="text"
          lable="Имя"
          id="first_name"
        />      
        <base-input
          type="text"
          lable="Отчество"
          id="third_name"
        />
      </div>
      <div 
        class="form__birthday"
      >
        <base-input
          type="date"
          lable="Дата рождения"
          id="birthday"
        />      
      </div>

      <div 
        class="form__email"
      >
        <base-input
          type="email"
          lable="E-mail"
          id="email"
        />      
      </div>

    </div>

    <div class="form__item">
      <div class="form__item-header">Паспортные данные</div>
        <div 
          class="form__birthday"
        >
          <base-multi-select
            lable="Гражданство"
            :items="citizenships"
            prop-name="nationality"
            :selected="selectedСitizenships"
            @update="updateCitizenships"
          />
        </div>
        <form-russian-citizenship
          v-if="isRussian"
        />
        <form-other-citizenship
          v-else
        />
    </div>

  </div>
</template>

<script>
import BaseInput from './BaseInput'
import FormRussianCitizenship from './FormRussianCitizenship';
import FormOtherCitizenship from './FormOtherCitizenship';
import BaseMultiSelect from './BaseMultiSelect';
import citizenships from '../assets/data/citizenships.json'

export default {
  data() {
    return {
      citizenships,
      selectedСitizenships: {}
    };
  },
  components: {
    BaseInput,
    BaseMultiSelect,
    FormRussianCitizenship,
    FormOtherCitizenship,
  },
  created() {
    if(this.citizenships.length) {
      this.selectedСitizenships = this.citizenships[0]
    }
  },
  methods: {
    updateCitizenships(item) {
      this.selectedСitizenships = item
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
}

.form__email {
  display: grid;
  grid-template-columns: 1fr;
}
</style>
