<template>
  <div>
    <p>Completed Tasks: {{todos.filter(todo => {return todo.done === true}).length}}</p>
    <p>Pending Tasks: {{todos.filter(todo => {return todo.done === false}).length}}</p>

    <todo v-on:delete-todo="deleteTodo" v-on:complete-todo="completeTodo" v-for="todo in todos" :todo.sync="todo"></todo>

  </div>
</template>

<script type="text/javascript">
import sweetalert from "sweetalert";
import Todo from "./Todo";

export default {
  props: ["todos"],
  components: {
    Todo
  },
  methods: {
    deleteTodo(todo) {
      swal({
        title: "Are you sure",
        text: "This To-Do will be permanently deleted!",
        icon: "warning",
        buttons: true,
        dangerMode: true,
        buttons: ["Cancel", "Yes, delete it!"]
      }).then(willDelete => {
        if (willDelete) {
          const todoIndex = this.todos.indexOf(todo);
          this.todos.splice(todoIndex, 1);
          swal("Deleted!", "Your To-Do has been deleted.", "success");
        }
      });
    },
    completeTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos[todoIndex].done = true;
      swal("Success!", "To-Do completed!", "success");
    }
  }
};
</script>
