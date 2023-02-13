<template>
  <form class="card" @submit.prevent="submitHandler">
    <div class="card__wrapper">
      <div class="card__header--title">Введите данные</div>
      <hr>
    <div class="card__header">
      <div class="card__header--form" :class="{invalid: errors.surname}">
        Фамилия*
        <input type="text" 
          placeholder="Фамилия" 
          v-model.trim="surname"
        >
        <small v-if="errors.name">{{ errors.surname }}</small>
      </div>
      <div class="card__header--form" :class="{invalid: errors.name}">
        Имя*
        <input type="text" 
          placeholder="Имя" 
          v-model.trim="nameClient"
        >
        <small v-if="errors.name">{{ errors.name }}</small>
      </div>
      <div class="card__header--form">
        Отчество
        <input type="text" 
          placeholder="Отчество"
          v-model.trim="patronymic"
        >
      </div>
      <div class="card__header--form" :class="{invalid: errors.date}">
        Дата рождения*
        <input type="date" 
          v-model="date"
        >
        <small v-if="errors.name">{{ errors.date }}</small>
      </div>
      <div class="card__header--form" :class="{invalid: errors.tel}">
        Номер телефона*
        <input type="tel" placeholder="+7 900 000 00 00" 
          v-model="tel"
        >
        <small v-if="errors.tel">{{ errors.tel }}</small>
      </div>
      <div class="card__header--form">
        Пол
        <div class="sex">
          <label><input type="radio" v-model="sex" value="male" name="sex"/>Мужчина</label>
          <label><input type="radio" v-model="sex" value="female" name="sex">Женщина</label>
        </div>
      </div>
      <div class="card__header--form">
        <label for="clients">Группа клиентов*</label>
        <select name="clients" id="clients-select" v-model="clients">
          <option value="omc">ОМС</option>  
          <option value="vip">VIP</option>
          <option value="problems">Проблемные</option>
        </select>
      </div>
      <div class="card__header--form" :class="{invalid: errors.doctor}">
        <label for="doctor">Лечащий врач*</label>
        <select name="doctor" id="doctor-select" v-model="doctor">
            <optgroup label="--Выберите лечащего врача--"></optgroup>
          <option value="doc1">Иванов</option>
          <option value="doc2">Захаров</option>
          <option value="doc3">Чернышева</option>
        </select>
        <small v-if="errors.doctor">{{ errors.doctor }}</small>
      </div>
      <div class="card__header--form">
        <div>
          <label><input type="checkbox" v-model="sms">Не отправлять смс</label>
        </div>
      </div>
    </div>
    </div>
    <div class="card__wrapper">
      <div class="card__header--title">Адрес</div>
      <hr>
    <div class="card__header">
      <div class="card__header--form">
        Индекс
        <input 
          id="index" 
          type="number" 
          maxlength="6" 
          placeholder="100100"
          v-model.number="index"
        >
      </div>
      <div class="card__header--form">
        Страна
        <input type="text" 
          placeholder="Россия"
          v-model="country"
        >
      </div>
      <div class="card__header--form">
        Область
        <input type="text" 
          placeholder="Курская область"
          v-model="region"
        >
      </div>
      <div class="card__header--form" :class="{invalid: errors.city}">
        Город*
        <input type="text" 
          placeholder="Курск" 
          v-model="city"
        >
        <small v-if="errors.city">{{ errors.city }}</small>
      </div>
      <div class="card__header--form">
        Улица
        <input type="text" 
          placeholder="ул. им Ленина"
          v-model="street"
        >
      </div>
      <div class="card__header--form">
        Дом
        <input type="text" 
          placeholder="1"
          v-model="home"
        >
      </div>
    </div>
    </div>
    <div class="card__wrapper">
      <div class="card__header--title">Паспорт</div>
      <hr>
    <div class="card__header">
      <div class="card__header--form" :class="{invalid: errors.docs}">
        <label for="docs">Тип документа*</label>
        <select name="docs" id="docs-select" >
          <option value="docs1">Паспорт</option>
          <option value="docs2">Свидетельство о рождении</option>
          <option value="docs3">Вод. удостоверение</option>
        </select>
        <small v-if="errors.docs">{{ errors.docs }}</small>
      </div>
      <div class="card__header--form">
        Серия
        <input type="number" 
          maxlength="6" 
          placeholder="100100"
          v-model.number="series"
        >
      </div>
      <div class="card__header--form">
        Номер
        <input type="text" 
          maxlength="4" 
          placeholder="1010"
          v-model.number="issue"
        >
      </div>
      <div class="card__header--form">
        Кем выдан
        <input type="text" 
          placeholder="МВД по РФ"
          v-model.number="whom"
        >
      </div>
      <div class="card__header--form" :class="{invalid: errors.whomDate}">
        Дата выдачи*
        <input type="date" 
          v-model.number="whomDate"
        >
      </div>
      <small v-if="errors.whomDate">{{ errors.whomDate }}</small>
    </div>
    <button type="submit" class="submit">Отправить данные</button>
    <div>*Поле обязательное для заполнения.</div>
    </div>
  </form>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      surname: '',
      index: '',
      clients: 'omc',
      nameClient: '',
      patronymic: '',
      date: '',
      tel: '',
      doctor: 'doc1',
      country: '',
      region: '',
      city: '',
      street: '',
      home: '',
      docs: 'docs1',
      series: '',
      issue: '',
      whom: '',
      whomDate: '',
      sex: null,
      sms: null,
      errors: {
        name: null,
        surname: null,
        date: null,
        tel: null,
        clients: null,
        doctor: null,
        city: null,
        docs: null,
        whomDate: null
      }
    }
  },
  methods: {
    formIsValid() {
      let isValid = true
      if (this.nameClient.length === 0
        ) {
        this.errors.name = 'Введите ваше имя'
        isValid = false
      } else {
        this.errors.name = null
      }
      if (this.surname.length === 0) {
        this.errors.surname = 'Введите вашу фамилию'
        isValid = false
      } else {
        this.errors.surname = null
      }
      if (this.date.length === 0) {
        this.errors.date = 'Введите дату рождения'
        isValid = false
      } else {
        this.errors.date = null
      }
      if (this.tel.length === 0) {
        this.errors.tel = 'Введите ваш телфон'
        isValid = false
      } else {
        this.errors.tel = null
      }
      if (this.clients.length === 0) {
        this.errors.clients = 'Добавьте вашу группу'
        isValid = false
      } else {
        this.errors.clients = null
      }
      if (this.doctor.length === 0) {
        this.errors.doctor = 'Выберите врача'
        isValid = false
      } else {
        this.errors.doctor = null
      }
      if (this.city.length === 0) {
        this.errors.city = 'Добавьте город'
        isValid = false
      } else {
        this.errors.city = null
      }
      if (this.whomDate.length === 0) {
        this.errors.whomDate = 'Введите дату вычаи паспорта'
        isValid = false
      } else {
        this.errors.whomDate = null
      }
      return isValid
    },
    submitHandler() {
      if (this.formIsValid()) {
        console.log(this.nameClient);
        console.log(this.surname);
        console.log(this.date);
        console.log(this.tel);
        console.log(this.clients);
        console.log(this.doctor);
        console.log(this.city);
        console.log(this.docs);
        console.log(this.whomDate);
      }
    }
  }
}
</script>

<style lang="scss">
.card {
  border-radius: 20px;
  padding: 10px;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  &__wrapper {
    background-color: #fff;
    border: 1px solid #313cce;
    border-radius: 20px;
    padding: 15px;
    margin-bottom: 5px;
    margin-right: 10px;
  }
  &__header{
    display: flex;
    flex-direction: column;
    margin-bottom: 5px;
    &--form {
      display: flex;
      justify-content: space-between;
      margin-bottom: 5px;
      flex-direction: column;
    }
    &--title {
      margin-bottom: 5px;
    }
  }
}
.card small {
  color: red;
}
.card__header--form.invalid input {
  border-color: red;
}
.submit {
  padding: 7px 10px;
  border-radius: 20px;
  cursor: pointer;
  border: none;
  background-color: #313cce;
  color: #fff;
}
.submit:hover {
  background-color: #5b64e2;
}
input[type="number"] {
	-moz-appearance: textfield;
	-webkit-appearance: textfield;
	appearance: textfield;
}
 
input[type="number"]::-webkit-outer-spin-button,
input[type="number"]::-webkit-inner-spin-button {
	display: none;
}
input {
  border-radius: 5px;
}
</style>
