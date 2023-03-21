<template>
  <input type="text" v-model="newTaskText" />
  <button type="button" @click="handleClick">Criar Task</button>

  <ul>
    <li v-for="task in allTasks" v-bind:key="task.id" v-bind:id="task.id">
      <span @click="handleCompleteTask">{{ task.text }}</span>
      <button @click="deleteTask">Apagar Task</button>
    </li>
  </ul>
</template>

<script lang="ts">
import { defineComponent } from "vue"

export default defineComponent({
  data() {
    return {
      counter: 0,
      newTaskText: '',
      allTasks: [] as {id:string, text: string}[]
    }
  },
  methods: {
    handleClick() {
      const newTask = {
        id: String(new Date().getTime()),
        text: this.newTaskText
      }
      this.allTasks = [...this.allTasks, newTask]
    },
    handleCompleteTask(event: Event) {
      const target = event.target as HTMLSpanElement
      if (target) {
        target.classList.toggle('selecionado')
      }
    },
    deleteTask(event: Event) {
      const target = event.target as HTMLElement
      if (target) {
        const parentElement = target.parentElement as HTMLElement
        const allTasksWithoutTheRemoved = this.allTasks.filter((task) => task.id !== parentElement.id)
        this.allTasks = allTasksWithoutTheRemoved
      }

    }
  }
})
</script>

<style>
  .selecionado {
    font-weight: bold;
    text-decoration: line-through;
  }
</style>