<template>
  <div class="form">
    <h1 class="form__title">Личные данные</h1>
    <oz-row>
      <oz-form-group class="form__group">
        <template #label>
          <label for="lastName">Фамилия</label>
        </template>
        <oz-input id="lastName" v-model="formData.lastName"></oz-input>
      </oz-form-group>
      <oz-form-group class="form__group">
        <template #label>
          <label for="firstName">Имя</label>
        </template>
        <oz-input id="firstName" v-model="formData.firstName"></oz-input>
      </oz-form-group>
      <oz-form-group class="form__group">
        <template #label>
          <label for="middleName">Отчество</label>
        </template>
        <oz-input id="middleName" v-model="formData.middleName"></oz-input>
      </oz-form-group>
    </oz-row>
    <oz-row>
      <oz-form-group class="form__group">
        <template #label>
          <label for="birthdate">Дата рождения</label>
        </template>
        <oz-date-input id="birthdate" v-model="formData.birthdate"></oz-date-input>
      </oz-form-group>
    </oz-row>
    <oz-row>
      <oz-form-group class="form__group">
        <template #label>
          <label for="email">E-mail</label>
        </template>
        <oz-email-input id="email" v-model="formData.email"></oz-email-input>
      </oz-form-group>
    </oz-row>
    <oz-row>
      <oz-form-group class="form__group">
        <template #label>
          <label for="sex">Пол</label>
        </template>
        <oz-radio-group id="sex" v-model="formData.sex" :items="['Мужской', 'Женский']"></oz-radio-group>
      </oz-form-group>
    </oz-row>
    <h1 class="form__title">Паспортные данные</h1>
    <oz-row>
      <oz-form-group class="form__group">
        <template #label>
          <label for="citizen">Гражданство</label>
        </template>
        <oz-select id="citizen" name="nationality" v-model="formData.citizen" :items="citizenItems" style="width: 300px;"></oz-select>
      </oz-form-group>
    </oz-row>
    <template v-if="formData.citizen === 'Russia'">
      <oz-row>
        <oz-form-group class="form__group">
          <template #label>
            <label for="passport_seria">Серия паспорта</label>
          </template>
          <oz-input id="passport_seria" v-model="formData.passport.seria"></oz-input>
        </oz-form-group>
        <oz-form-group class="form__group">
          <template #label>
            <label for="passport_number">Номер паспорта</label>
          </template>
          <oz-input id="passport_number" v-model="formData.passport.number"></oz-input>
        </oz-form-group>
        <oz-form-group class="form__group">
          <template #label>
            <label for="passport_date">Дата выдачи</label>
          </template>
          <oz-date-input id="passport_date" v-model="formData.passport.date"></oz-date-input>
        </oz-form-group>
      </oz-row>
    </template>
    <template v-else-if="formData.citizen">
      <oz-row>
        <oz-form-group class="form__group">
          <template #label>
            <label for="lastName_eng">Фамилия на латинице</label>
          </template>
          <oz-input id="lastName_eng" v-model="formData.lastName_eng"></oz-input>
        </oz-form-group>
        <oz-form-group class="form__group">
          <template #label>
            <label for="firstName_eng">Имя на латинице</label>
          </template>
          <oz-input id="firstName_eng" v-model="formData.firstName_eng"></oz-input>
        </oz-form-group>
      </oz-row>
      <oz-row>
        <oz-form-group class="form__group">
          <template #label>
            <label for="passport_number">Номер паспорта</label>
          </template>
          <oz-input id="passport_number" v-model="formData.passport.number"></oz-input>
        </oz-form-group>
        <oz-form-group class="form__group">
          <template #label>
            <label for="passport_country">Страна выдачи</label>
          </template>
          <oz-select id="passport_country" name="flag" v-model="formData.passport.country" :items="citizenItems"></oz-select>
        </oz-form-group>
        <oz-form-group class="form__group">
          <template #label>
            <label for="passport_date">Тип паспорта</label>
          </template>
          <oz-select id="passport_date" name="type" v-model="formData.passport.type" :items="passportTypes"></oz-select>
        </oz-form-group>
      </oz-row>
    </template>
    <oz-row>
      <oz-form-group class="form__group">
        <template #label>
          <label for="changeFIO">Меняли ли фамилию или имя?</label>
        </template>
        <oz-radio-group id="changeFIO" v-model="formData.changeFIO" :items="['Нет', 'Да']"></oz-radio-group>
      </oz-form-group>
    </oz-row>
    <template v-if="formData.changeFIO === 'Да'">
      <oz-row>
        <oz-form-group class="form__group">
          <template #label>
            <label for="lastName_new">Предыдущая Фамилия</label>
          </template>
          <oz-input id="lastName_new" v-model="formData.lastName_new"></oz-input>
        </oz-form-group>
        <oz-form-group class="form__group">
          <template #label>
            <label for="firstName_new">Предыдущее Имя</label>
          </template>
          <oz-input id="firstName_new" v-model="formData.firstName_new"></oz-input>
        </oz-form-group>
      </oz-row>
    </template>
    <oz-row>
      <button @click="submit">Отправить</button>
    </oz-row>
  </div>
</template>

<script>
import citizenItems from "/src/assets/data/citizenships.json";
import passportTypes from "/src/assets/data/passport-types.json";

import {
  OzRow,
  OzFormGroup,
  OzInput,
  OzDateInput,
  OzEmailInput,
  OzRadioGroup,
  OzSelect,
} from "./FormItems";

export default {
  components: {
    OzRow,
    OzFormGroup,
    OzInput,
    OzDateInput,
    OzEmailInput,
    OzRadioGroup,
    OzSelect,
  },

  data() {
    return {
      formData: {
        lastName: "",
        firstName: "",
        middleName: "",
        birthdate: "",
        email: "",
        sex: "",
        citizen: "",
        passport: {
          seria: "",
          number: "",
          date: "",
          country: "",
          type: "",
        },
        lastName_eng: "",
        firstName_eng: "",
        middleName_eng: "",
        lastName_new: "",
        firstName_new: "",
      },
      citizenItems,
      passportTypes,
    };
  },
  methods: {
    onit(items) {
      for (const item of items) {
        this.formData[item] = "";
      }
    },
    submit () {
      console.log('Отправляемые данные', JSON.stringify(this.formData))
    }
  },
};
</script>

<style scoped>
.form {
}

.form__group {
  flex: 1;
}
</style>
