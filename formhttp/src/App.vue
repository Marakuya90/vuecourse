<template>
  <div class="container mt-5 pt-5 pb-5 ps-4 pe-4">
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
<app-people-list
    :people="people"
    @load="listPeopleLoader"
    @delete="deletePerson"
>
</app-people-list>
  </div>
</template>

<script>
import AppPeopleList from "@/components/AppPeopleList.vue";
import axios from "axios";
// import axios from "axios";

export default {
  data() {
    return {
      name: '',
      people: []
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
              'Content-Type':'application/json'},
            body: JSON.stringify({
              firstName: this.name,
            })
          })

      const firebaseData = await response.json()
      this.people.push({
        firstName: this.name,
        id:firebaseData.name
      })
      this.name = ''
    },

    //запрос с помощью axios
    // async listPeopleLoader() {
    //   await axios.get('https://vue-with-http-7e764-default-rtdb.europe-west1.firebasedatabase.app/people.json')
    // },

    async listPeopleLoader() {
      try {
        const response = await fetch('https://vue-with-http-7e764-default-rtdb.europe-west1.firebasedatabase.app/people.json', {
          method:'GET'
        })
        const listPeople = await response.json()
        console.log(listPeople)
        this.people = Object.keys(listPeople).map(key => {
          return {
            id: key,
            //...listPeople[key]
            firstName: listPeople[key].firstName
          }
        })
      } catch (e) {
        console.log(e.message)
      }
    },
    async deletePerson(id) {
      await axios.delete(`https://vue-with-http-7e764-default-rtdb.europe-west1.firebasedatabase.app/people/${id}.json`)
    console.log(id)
      this.people = this.people.filter(person => person.id !== id)
    }
  },
  components: { AppPeopleList }
}
</script>

<style scoped>
div {
  border-radius: 10px;
  background-color: #FFFFFF;

}
</style>
