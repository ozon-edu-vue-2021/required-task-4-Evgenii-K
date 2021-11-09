<template>
    <div class="form__item">
      <div class="form__passport-russian">
        <base-input
          type="number"
          label="Серия паспорта"
          id="passport_series_russian"
          v-model="passport.series"
          v-mask="'####'"
          @input="update"
          required
          :error="errors.series"
        />      
        <base-input
          type="number"
          label="Номер паспорта"
          id="passport_number_russian"
          v-model="passport.number"
          v-mask="'######'"
          @input="update"
          required
          :error="errors.number"
        />      
        <base-input
          type="date"
          label="Дата выдачи"
          id="date_of_issue"
          v-model="passport.date"
          @input="update"
          required
          :max="todaysDay"
        />
      </div>
    </div>
</template>

<script>
import BaseInput from '../BaseComponents/BaseInput'
import { VueMaskDirective } from "v-mask"
import TodaysDate from '../../utils/TodaysDate.vue'

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
  props: {
    errors: {
      type: Object,
      default: () => ({})
    }
  },
  mixins: [ TodaysDate ],
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
