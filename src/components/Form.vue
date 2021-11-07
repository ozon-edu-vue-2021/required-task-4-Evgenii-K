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
          id="second_name"
        />      
      </div>
    </div>

    <div class="form__item">
      <div class="form__item-header">Паспортные данные</div>
        <div 
          class="form__birthday"
        >
          <base-dropdown
            lable="Гражданство"
            id="citizenship"
          />      
        </div>
        <form-russian-citizenship/>
    </div>

  </div>
</template>

<script>
import BaseInput from './BaseInput'
import BaseDropdown from './BaseDropdown'
import FormRussianCitizenship from './FormRussianCitizenship.vue';
export default {
  data() {
    return {};
  },
  components: {
    BaseInput,
    BaseDropdown,
    FormRussianCitizenship,
  },
  methods: {},
};
</script>

<style scoped>
.form {
  display: grid;
  grid-gap: 20px;
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
</style>
