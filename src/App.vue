<template>
  <div class="container">
    <h1>Tambah Kegiatan</h1>
    <input type="text" v-model="newTodo" @keyup.enter="addTodo" placeholder="Tambah kegiatan baru...">
    <div v-for="(todo, index) in todos" :key="index" class="todo-item" :class="{ 'completed': todo.completed }">
      <input type="checkbox" v-model="todo.completed"> {{ todo.text }}
      <button @click="cancelTodo(index)">Batalkan</button>
      <button @click="editTodo(index)">Edit</button>
      <button @click="deleteTodo(index)">Hapus</button>
    </div>
    <button @click="filterTodos">Filter Belum Selesai</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: '',
      todos: []
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== '') {
        this.todos.push({ text: this.newTodo, completed: false });
        this.newTodo = '';
      }
    },
    cancelTodo(index) {
      this.todos.splice(index, 1);
    },
    editTodo(index) {
      const newText = prompt('Edit kegiatan:', this.todos[index].text);
      if (newText !== null) {
        this.todos[index].text = newText;
      }
    },
    deleteTodo(index) {
      if (confirm('Apakah Anda yakin ingin menghapus kegiatan ini?')) {
        this.todos.splice(index, 1);
      }
    },
    filterTodos() {
      this.todos = this.todos.filter(todo => !todo.completed);
    }
  }
}
</script>

<style scoped>
.container h1{
  color: #000;
}
.container {
  max-width: 600px;
  margin: 20px auto;
  background-color: #fff;
  padding: 20px;
  border-radius: 5px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.todo-item {
  margin-bottom: 10px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #f9f9f9;
  color: #000;
}

.completed {
  text-decoration: line-through;
  color: #000;
}
</style>
