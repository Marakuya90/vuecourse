<template>
<div class="container">
  <h2 class="mb-4">Анкета на VUE разработчика</h2>
  <form action="#" @submit.prevent="submitHandler">
    <app-input
        type="text"
        placeholder="Введи имя"
        :error="errors.name"
        label="Как тебя зовут?"
        v-model="name"
        margin="mb-3"
    ></app-input>
    <app-input
        type="number"
        label="Выбери возраст"
        v-model=age
        margin="mb-3"
        max="70"
    ></app-input>
    <div class="form-control">
    <label class="form-label" for="city">Выбери город</label>
    <select
        class="form-select mb-3"
        id="city"
        v-model="city">
      <option value="nsk">Новосибирск</option>
      <option value="msk">Москва</option>
      <option value="spb">Санкт-Петербург</option>
    </select>
    </div>
    <div class="form-control">
    <h4>Ты готов к переезду в Токио</h4>
      <div id="moving" class="d-flex flex-column">
        <div>
          <label class="form-label"><input
              type="radio"
              id="yes"
              class="form-check-input me-3"
              name="relocate"
              value="yes"
              v-model="relocate"/>Да</label>
        </div>
      <div>
        <label class="form-label">
          <input
            type="radio"
            id="no"
            class="form-check-input me-3"
            name="relocate"
            value="no"
            v-model="relocate"/>Нет</label>
      </div>
      </div>
    </div>

    <div class="form-control mb-2">
    <h4>Что знаешь во VUE?</h4>
        <div class="d-flex flex-column">
          <section>
            <label class="form-label">
              <input
                  class="form-check-input me-3"
                  type="checkbox"
                  value="vuex"
                  v-model="skills"
                  name="skills"
              />Vuex</label>
          </section>

          <section>
          <label class="form-label">
            <input
                class="form-check-input me-3"
                type="checkbox"
                value="cli"
                v-model="skills"
                name="skills"
            />Vue CLI</label>
          </section>

          <section>
          <label class="form-label" for="router">
            <input
                class="form-check-input me-3"
                type="checkbox"
                value="router"
                v-model="skills"
                name="skills"/>Vue Router</label>
          </section>

        </div>
    </div>
    <button
        type="submit"
        class="btn btn-outline-success"
    >Отправить</button>
  </form>
</div>
</template>

<script>
import AppInput from "@/components/AppInput.vue";
export default {
  name: "app-form",
  data() {
    return {
      name: '',
      age: 23,
      city: 'spb',
      relocate: 'yes',
      skills: [],
      errors: {
        name: null
      }
    }
  },
  methods: {
    formIsValid() {
      let isValid = true
      this.errors.name = 'Имя не может быть пустым'
      if(this.name.length === 0) {
        isValid = false
      } else {
        this.errors.name = null
      }
       return isValid
    },
    submitHandler() {
      if(this.formIsValid()) {
        console.group('Form Data')
        console.log('Name:', this.name)
        console.log('Age:', this.age)
        console.log('City:', this.city)
        console.log('Relocate:', this.relocate)
        console.log('Skills:', this.skills)
        console.groupEnd()
      }
    }
  },
    components: {AppInput}
}
</script>

<style>
.form-control small {
  color: darkred;
}
.form-control.invalid input {
  border-color: darkred;
  border-width: 2px;
}
</style>
