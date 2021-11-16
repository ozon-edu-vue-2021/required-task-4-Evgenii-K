<script>
import { minLength } from 'vuelidate/lib/validators'

const alphaCyrillic = {
  alpha: val => /^[а-яё]*$/i.test(val),
}

const alphaLetters = {
  alpha: val => /^[a-z]*$/i.test(val),
}

const emailRegex = {
  alpha: val => /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/.test(val)
} 

export default {
  validations: {
    formData: {
      firstName: alphaCyrillic,
      secondName: alphaCyrillic,
      thirdName: alphaCyrillic,
      email: emailRegex,
    },
    passport: {
      russian: {
        series: {
          minLength: minLength(4)
        },
        number: {
          minLength: minLength(6)
        },
      },
      foreign: {
        secondName: alphaLetters,
        firstName: alphaLetters,
      }
    },
  },
  computed: {
    errors() {

      const textOfError = {
        firstName: null,
        secondName: null,
        thirdName: null,
        email: null,
        
        russian: {
          series: null,
          number: null
        },

        foreign: {
          secondName: null,
          firstName: null,
        }
      };

      ['firstName', 'secondName', 'thirdName'].forEach(name => {
        if (!this.$v.formData[name].alpha && this.$v.formData[name].$dirty) {
          textOfError[name] = 'Только кириллица'
        }
      });

      if (!this.$v.formData.email.alpha && this.$v.formData.email.$dirty) {
        textOfError.email = 'Не валидный почтовый адрес'
      };

      if (!this.$v.passport.russian.series.minLength && this.$v.passport.russian.series.$dirty) {
        textOfError.russian.series = 'Не менее 4 цифр'     
      };
      
      if (!this.$v.passport.russian.number.minLength && this.$v.passport.russian.number.$dirty) {
        textOfError.russian.number = 'Не менее 6 цифр'
      };
        

      ['firstName', 'secondName'].forEach(name => {
        if (!this.$v.passport.foreign[name].alpha && this.$v.passport.foreign[name].$dirty) {
          textOfError.foreign[name] = 'Только латинский алфавит'
        };
      });

      return textOfError
    },
  }
}
</script>