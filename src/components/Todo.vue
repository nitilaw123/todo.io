<template>
  <div id="app">
    <h2>To do: ({{ todos.length }})</h2>
    <input
      type="text"
      v-model="todo"
      placeholder="Type something and press ENTER"
      v-on:keyup.enter="add"
    />
    <ol>
      <li v-for="todo in todos" :key="todo.text">
        <label>
          <input type="checkbox" @click="completeditem(todo.text)" />
          <span>{{ todo.text }}</span>
          <a
            href="#"
            class="remove"
            v-on:click.prevent="remove($event, todo.text)"
            >Remove</a
          >
        </label>
      </li>
    </ol>
    <hr />
    <h2>Completed items: ({{ this.completed.length }})</h2>
    <ol>
      <li v-for="complete in completed" :key="complete.text">
        <label>
          <input type="checkbox" checked />
          <span>{{ complete.text }}</span>
          <a href="#" class="remove">Remove</a>
        </label>
      </li>
    </ol>
  </div>
</template>

<script>
export default {
  name: "Todo",
  data() {
    return {
      todo: "",
      completed: [],
      todos: [
        { text: "Send job application" },
        { text: "Learn about Vue" },
        { text: "Learn about Fliplet" },
        { text: "Play around in JSFiddle" },
        { text: "Show us what you've got" },
      ],
    };
  },
  methods: {
    add() {
      this.todos.push({ text: this.todo });
      this.todo = "";
    },
    remove(event, val) {
      event.target.this.todos = this.todos.filter((todo) => todo.text !== val);
    },
    completeditem(val2) {
      this.completed.push({ text: val2 });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
body {
  background: #20262E;
  padding: 20px;
  font-family: Helvetica;
}

#app {
  background: #fff;
  border-radius: 4px;
  padding: 20px;
  transition: all 0.2s;
}

li {
  margin: 8px 0;
}

h2 {
  font-weight: bold;
  margin-bottom: 15px;
}

del {
  color: rgba(0, 0, 0, 0.3);
}

input[type="text"] {
  padding: 10px;
  width: 200px;
}

label .remove {
  display: none;
  color: red;
}

label:hover .remove {
  display: inline-block;
  margin-left: 10px;
  color: red;
  opacity: 0.5;
}
</style>
