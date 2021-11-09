<template>
  <div class="form">
    <form @submit.prevent="handleSubmit">
      <div class="form-block">
        <p class="form-block__title">Личные данные</p>
        <div class="form-row">
          <div class="form-input">
            <label for="surname-input">Фамилия</label>
            <input
              v-model="formData.personalData.surname"
              type="text"
              id="surname-input"
              placeholder="Фамилия"
            />
          </div>
          <div class="form-input">
            <label for="name-input">Имя</label>
            <input
              v-model="formData.personalData.name"
              type="text"
              id="name-input"
              placeholder="Имя"
            />
          </div>
          <div class="form-input">
            <label for="middlename-input">Отчество</label>
            <input
              v-model="formData.personalData.middlename"
              type="text"
              id="middlename-input"
              placeholder="Отчество"
            />
          </div>
        </div>
        <div class="form-row">
          <div class="form-input">
            <label for="date-of-birth-input">Дата рождения</label>
            <input
              v-model="formData.personalData.dateBirth"
              type="date"
              id="date-of-birth-input"
              placeholder="Дата рождения"
            />
          </div>
        </div>
        <div class="form-row">
          <div class="form-input form-input_full-width">
            <label for="email-input">E-mail</label>
            <input
              v-model="formData.personalData.email"
              type="email"
              id="email-input"
              placeholder="Почта"
            />
          </div>
        </div>
      </div>
      <div class="form-block">
        <p class="form-block__title">Пол</p>
        <div class="form-row">
          <div class="form-radio-input">
            <input
              v-model="formData.personalData.gender"
              value="male"
              name="gender"
              checked
              type="radio"
              id="gender-input-1"
            />
            <label for="gender-input-1">Мужской</label>
          </div>
          <div class="form-radio-input">
            <input
              v-model="formData.personalData.gender"
              value="female"
              name="gender"
              type="radio"
              id="gender-input-2"
            />
            <label for="gender-input-2">Женский</label>
          </div>
        </div>
      </div>
      <div class="form-block">
        <p class="form-block__title">Паспотные данные</p>
        <div class="form-row">
          <div class="form-input">
            <label for="citizenship-input">Гражданство</label>
            <input
              id="citizenship-input"
              v-model="formData.passportData.citizenship"
              list="citi"
            />
            <datalist id="citi">
              <option
                v-for="citizenship in citizenships"
                :key="citizenship.uid"
                :value="citizenship.nationality"
              >
                {{ citizenship.flag }}
              </option>
            </datalist>
          </div>
        </div>
        <div v-if="isRussianCitizenship" class="form-row">
          <div class="form-input">
            <label for="pasport-series-input">Серия паспорта</label>
            <input
              v-model="formData.passportData.series"
              type="text"
              id="pasport-series-input"
              placeholder="Серия паспорта"
            />
          </div>
          <div class="form-input">
            <label for="pasport-id-input">Номер паспорта</label>
            <input
              v-model="formData.passportData.id"
              type="text"
              id="pasport-id-input"
              placeholder="Номер паспорта"
            />
          </div>
          <div class="form-input">
            <label for="pasport-date-input">Дата выдачи</label>
            <input
              v-model="formData.passportData.date"
              type="date"
              id="pasport-date-input"
              placeholder="Дата выдачи"
            />
          </div>
        </div>
        <template v-else>
          <div class="form-row">
            <div class="form-input">
              <label for="roman-surname-input">Фамилия на латинице</label>
              <input
                v-model="formData.passportData.romanSurname"
                id="roman-surname-input"
              />
            </div>
            <div class="form-input">
              <label for="roman-name-input">Имя на латинице</label>
              <input
                v-model="formData.passportData.romanName"
                id="roman-name-input"
              />
            </div>
          </div>
          <div class="form-row">
            <div class="form-input">
              <label for="pasport-id-input">Номер паспорта</label>
              <input
                v-model="formData.passportData.id"
                type="text"
                id="pasport-id-input"
                placeholder="Номер паспорта"
              />
            </div>
            <div class="form-input">
              <label for="passport-type-input">Тип паспорта</label>
              <select
                v-model="formData.passportData.countryOfIssue"
                id="passport-type-input"
              >
                <option
                  v-for="passportType in passportTypes"
                  :key="passportType.id"
                  :value="passportType.type"
                >
                  {{ passportType.type }}
                </option>
              </select>
            </div>
            <div class="form-input">
              <label for="country-of-issue-input">Страна выдачи</label>
              <input
                id="country-of-issue-input"
                v-model="formData.passportData.passportType"
                list="country-of-issue"
              />
              <datalist id="country-of-issue">
                <option
                  v-for="citizenship in citizenships"
                  :key="citizenship.uid"
                  :value="citizenship.nationality"
                >
                  {{ citizenship.flag }}
                </option>
              </datalist>
            </div>
          </div>
        </template>
      </div>
      <div class="form-block">
        <p class="form-block__title">Меняли ли фамилию или имя?</p>
        <div class="form-row">
          <div class="form-radio-input">
            <input
              v-model="formData.isChangeName"
              :value="false"
              name="gender1"
              type="radio"
              id="is-change-name-input-1"
            />
            <label for="is-change-name-input-1">Нет</label>
          </div>
          <div class="form-radio-input">
            <input
              v-model="formData.isChangeName"
              :value="true"
              name="gender1"
              type="radio"
              id="is-change-name-input-2"
            />
            <label for="is-change-name-input-2">Да</label>
          </div>
        </div>
        <div v-if="formData.isChangeName" class="form-row">
          <div class="form-input">
            <label for="prev-surname-input">Фамилия</label>
            <input
              v-model="formData.prevSurname"
              type="text"
              placeholder="Фамилия"
              id="prev-surname-input"
            />
          </div>
          <div class="form-input">
            <label for="prev-name-input">Фамилия</label>
            <input
              v-model="formData.prevName"
              type="text"
              placeholder="Имя"
              id="prev-name-input"
            />
          </div>
        </div>
      </div>
      <button type="submit">Send</button>
    </form>
  </div>
</template>

<script>
import allCitizenships from "../assets/data/citizenships.json";
import allPasportTypes from "../assets/data/passport-types.json";

export default {
  data() {
    return {
      citizenships: allCitizenships,
      passportTypes: allPasportTypes,
      formData: {
        personalData: {
          name: "",
          surname: "",
          middlename: "",
          dateBirth: "",
          email: "",
          gender: "male",
        },
        passportData: {
          citizenship: "Russia",
          series: "",
          id: "",
          date: "",
          romanSurname: "",
          romanName: "",
          countryOfIssue: "",
          passportType: "",
        },
        prevSurname: "",
        prevName: "",
        isChangeName: false,
      },
    };
  },
  computed: {
    isRussianCitizenship() {
      return this.formData.passportData.citizenship === "Russia";
    },
  },
  methods: {
    handleSubmit() {
      console.log(JSON.stringify(this.formData, null, 2));
    },
  },
};
</script>

<style scoped>
.form {
  width: 800px;
  margin: 0 auto;
}

.form-row {
  display: flex;
  margin-bottom: 10px;
}

.form-block {
  margin-bottom: 15px;
}

.form-block__title {
  font-weight: bold;
  font-size: 1.2rem;
  margin: 0;
  margin-bottom: 10px;
}

.form-input {
  margin-right: 20px;
  display: flex;
  flex-direction: column;
}

.form-input_full-width {
  width: 100%;
}

.form-input label {
  margin-bottom: 5px;
}

.form-radio-input {
  margin-right: 10px;
}

.form-radio-input input {
  margin-right: 5px;
}
</style>
