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
  name: "App",

  //#region DATA
  data() {
    return {
      title: "Cosa devo fare per imparare a guidare la macchina?",
      newTodo: "",
      todoList: [
        {
          text: "Imparare a partire da fermo",
          done: true,
        },
        {
          text: "Imparare a cambiare le marce",
          done: true,
        },
        {
          text: "Imparare frenare",
          done: false,
        },
        {
          text: "Imparare a scalare le marce",
          done: false,
        },
        {
          text: "Imparare a parcheggiare",
          done: false,
        },
      ],
    };
  },
  //#endregion DATA

  //#region METHODS
  methods: {
    addTask(task) {
      if (task.length >= 10) {
        const newtask = { text: task, done: false };
        this.todoList.push(newtask);
        this.newTodo = "";
        console.log(
          `Added element '${task}' in position ${this.todoList.length - 1}`
        );
      } else {
        alert("La lunghezza minima deve essere di almeno 10 caratteri");
        console.log(`Task '${task}' not added because too short`);
      }
    },
    removeTask(task, i) {
      this.todoList.splice(i, 1);
      console.log(`Removed element '${task.text}' in position ${i}`);
    },
    toggleDone(task, i) {
      task.done
        ? (this.todoList[i].done = false)
        : (this.todoList[i].done = true);
      console.log(
        `L'elemento '${task.text}' è ora ${task.done ? "fatto" : "da fare"}`
      );
    },
  },
  //#endregion
};
</script>

<template>
  <h1>{{ title }}</h1>

  <div class="new-task">
    <input
      type="text"
      placeholder="Inserisci un nuovo task"
      v-model="newTodo"
      @keyup.enter="addTask(newTodo)"
    />
    <button @click="addTask(newTodo)">Aggiungi</button>
  </div>

  <ul>
    <li v-for="(todo, index) in todoList" :class="todo.done ? 'todo-done' : ''">
      <div class="tagRemove" @click="removeTask(todo, index)">
        <i class="fa-solid fa-xmark"></i>
      </div>
      <span @click="toggleDone(todo, index)">{{ todo.text }}</span>
      <span
        v-if="todo.done"
        :class="'color-green'"
        @click="toggleDone(todo, index)"
        ><i class="fa-regular fa-square-check"></i
      ></span>
      <span
        v-else="todo.done"
        :class="'color-red'"
        @click="toggleDone(todo, index)"
        ><i class="fa-regular fa-square"></i
      ></span>
    </li>
  </ul>
</template>

<style>
button {
  margin-left: 1rem;
}
* {
  list-style: none;
}
li {
  display: flex;
  gap: 0.5rem;
  margin-block: 1rem;
}
span,
.tagRemove {
  cursor: pointer;
}
.tagRemove {
  background: red;
  color: white;
  border-radius: 5px;
  padding-inline: 0.4rem;
}
.todo-done {
  text-decoration: line-through;
}
.color-green {
  color: green;
}
.color-red {
  color: red;
}
</style>
