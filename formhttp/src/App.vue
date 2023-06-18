<template>
  <div class="container mt-5 pt-5 pb-5 ps-4 pe-4">
    <app-alert
        :alert = "alert"
        @close = "alert = null"
    ></app-alert>
    <h2>Работа с базой данных</h2>
    <hr/>

    <form @submit.prevent="createPerson">
      <div>
        <label class="form-label"
            for="name">Введите имя</label>
        <input class="form-control" type="text" id="name" v-model.trim="name">
      </div>
      <button class="btn btn-primary mt-4"
      :disabled="name.length === 0"
      >Cоздать</button>
    </form>
    <hr/>
    <app-loader v-if="loading"></app-loader>
    <app-people-list
        v-else
        :people="people"
        @load="listPeopleLoader"
        @delete="deletePerson">
    </app-people-list>
  </div>
</template>

<script>
import AppPeopleList from "@/components/AppPeopleList.vue";
import AppAlert from "@/components/AppAlert.vue";
import AppLoader from "@/components/AppLoader.vue";
import axios from "axios";


export default {
  data() {
    return {
      name: '',
      people: [],
      alert: null,
      loading: false
    }
  },
  mounted() {
    this.listPeopleLoader()
  },
  methods: {
    async createPerson() {
      const response = await fetch('https://vue-with-http-7e764-default-rtdb.europe-west1.firebasedatabase.app/people.json',
          {
            method: 'POST',
            headers: {
              'Content-Type': 'application/json'
            },
            body: JSON.stringify({
              firstName: this.name,
            })
          })

      const firebaseData = await response.json()
      this.people.push({
        firstName: this.name,
        id: firebaseData.name
      })
      this.name = ''
    },
    //запрос с помощью axios
    // async listPeopleLoader() {
    //   await axios.get('https://vue-with-http-7e764-default-rtdb.europe-west1.firebasedatabase.app/people.json')
    // },
    async listPeopleLoader() {
      try {
        this.loading = true
        const response = await fetch('https://vue-with-http-7e764-default-rtdb.europe-west1.firebasedatabase.app/people.json', {
          method: 'GET'
        })
        const listPeople = await response.json()
          if (!listPeople) {
            throw new Error('Список людей пуст!')
          }
        console.log(listPeople)
        this.people = Object.keys(listPeople).map(key => {
          return {
            id: key,
            //...listPeople[key]
            firstName: listPeople[key].firstName
          }
        })
        this.loading = false
      } catch (e) {
        this.alert = {
          type: 'alert-danger',
          title: 'Ошибка!',
          text: e.message
        }
        this.loading = false
      }
    },
    async deletePerson(id) {
      try {
        const name = this.people.find(person => person.id === id).firstName
        await axios.delete(`https://vue-with-http-7e764-default-rtdb.europe-west1.firebasedatabase.app/people/${id}.json`)
        console.log(id)
        this.people = this.people.filter(person => person.id !== id)
        this.alert = {
          type: 'alert-success',
          title: 'Успешно!',
          text: `Пользователь ${name} был удален!`
        }
      } catch (e) {
        console.log(e.message)
      }
    }
  },
  components: {AppPeopleList, AppAlert, AppLoader}
}
</script>

<style scoped>
div {
  border-radius: 10px;
  background-color: #FFFFFF;

}
</style>
