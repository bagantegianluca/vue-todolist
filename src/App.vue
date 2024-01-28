<!-- Descrizione:
Fare l'esercizio della to do list per ogni todo avremo un oggetto, formato da due proprietà:
text, una stringa che indica il testo del todo
done, un booleano (true/false) che indica se il todo è stato fatto oppure no
MILESTONE 1
Stampare all'interno di una lista HTML un item per ogni todo. Se la proprietà done è uguale a true, visualizzare il testo del todo sbarrato.
MILESTONE 2
Visualizzare a fianco ad ogni item ha una "x": cliccando su di essa, il todo viene rimosso dalla lista.
MILESTONE 3
Predisporre un campo di input testuale e un pulsante "aggiungi": cliccando sul pulsante, il testo digitato viene letto e utilizzato per creare un nuovo todo, che quindi viene aggiunto alla lista dei todo esistenti.
Bonus:
1- oltre al click sul pulsante, intercettare anche il tasto ENTER per aggiungere il todo alla lista
2- cliccando sul testo dell'item, invertire il valore della proprietà done del todo corrispondente (se done era uguale a false, impostare true e viceversa)
Nota:
Non ci sono nuovi concetti, ma solo quelli coperti fino ad oggi in vue.
Leggete la documentazione (É vostra amica), di seguito le pagine di riferimento che vi torneranno utili per svolgere l'esercizio.
https://vuejs.org/guide/essentials/template-syntax.html
https://vuejs.org/guide/essentials/class-and-style.html
https://vuejs.org/guide/essentials/conditional.html
https://vuejs.org/guide/essentials/list.html
https://vuejs.org/guide/essentials/event-handling.html
https://vuejs.org/guide/essentials/forms.html
-->

<script>
export default {
  name: 'App',
  data() {
    return {
      title: 'Cosa devo fare per imparare a guidare la macchina?',
      todoList: [
        {
          text: 'Imparare a partire da fermo',
          done: true
      },
      {
          text: 'Imparare a cambiare le marce',
          done: true
      },
      {
          text: 'Imparare frenare',
          done: false
      },
      {
          text: 'Imparare a scalare le marce',
          done: false
      },
      {
          text: 'Imparare a parcheggiare',
          done: false
      }
    ]
    }
  },
  methods: {
    removeTask(i) {
      console.log(`Removed elemente in position ${i}`);
      this.todoList.splice(i, 1);
    }
  }
}
</script>

<template>

<h1>{{ title }}</h1>

<ul>
  <li v-for="(todo, index) in todoList" :class="todo.done ? 'todo-done' : ''">
    <div class="tagRemove" @click="removeTask(index)"><i class="fa-solid fa-xmark"></i></div>
    {{ todo.text}}
  <span v-if="todo.done" :class="'color-green'"><i class="fa-regular fa-square-check"></i></span>
  <span v-else="todo.done" :class="'color-red'"><i class="fa-regular fa-square"></i></span>
  </li>
</ul>

</template>

<style>
*{list-style: none}
li{display: flex; gap: .5rem; margin-block: 1rem;}
.tagRemove{background: red; color: white; border-radius: 5px; padding-inline: .4rem; cursor: pointer;}
.todo-done{text-decoration: line-through;}
.color-green{color: green}
.color-red{color: red}
</style>
