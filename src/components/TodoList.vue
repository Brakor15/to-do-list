<script setup lang='ts'>
  import { ref } from 'vue'

  const id = ref(0)
  const newElement = ref('')

  const elements = ref([
    { id: id.value++, text: 'Faire les courses', done: false },
    { id: id.value++, text: 'Faire à manger', done: false },
  ])

  function addElement() {
    elements.value.push({ id: id.value++, text: newElement.value, done: false})
    newElement.value = ''
  }

  function removeElement(id: number) {
    elements.value = elements.value.filter((el) => el.id !== id)
  }

</script>

<template>
  <div class="wrapper">
    <div class="content">
      <h1>Liste de choses à faire</h1>
      <v-form @submit.prevent="addElement">
        <v-text-field v-model="newElement" required placeholder="Type here"/>
        <v-btn rounded="xl" type="submit">Add</v-btn>
      </v-form>
      <v-list>
        <v-list-item v-for="el in elements" :key="el.id" >
          <input type="checkbox" v-model="el.done" />
          <span :class="{ done: el.done}">{{ el.text }}</span>
          <v-btn rounded="xl" @click="removeElement(el.id)">X</v-btn>
        </v-list-item>
      </v-list>
    </div>
  </div>
</template>

<style>

.done {
  text-decoration: line-through;
}

h1 {
  font-family: FiraCode;
}

v-text-field {
  width: 300px;
}

.wrapper {
  background-color: purple;
  margin: 5%;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}

.content {
  width: 500px;
  margin: 100px;
  padding: 50px;
  background-color: white;
  color: black;
}

span {
  margin: 10px;
}

v-btn {
  font-family: FiraCode;
}

v-list-item {
  font-family: FiraCode;
}
</style>