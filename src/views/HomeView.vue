<template>
  <div class="home">
    <b-col class="d-flex justify-content-center">
      <b-row>
        <b-form-input
          v-model="textInput"
          placeholder="Input your todo"
          class="mx-4"
          @keydown.enter="addTodo(textInput)"
        ></b-form-input>
      </b-row>
      <b-button variant="success" @click="addTodo(textInput)" outline
        >Add</b-button
      >
    </b-col>
    <div>
      <b-col v-for="item in listTodo" :key="item.id" class="card-todo mx-auto">
        <div
          class="text-todo d-flex justify-content-between align-items-center mt-4 px-5 py-2 rounded"
        >
          <b-form-checkbox v-model="item.isDone"></b-form-checkbox>
          <div :class="[item.isDone ? `text-todo-done` : ``]">
            {{ item.text }}
          </div>
          <b-button variant="danger" @click="deleteTodo(item)">
            Delete
          </b-button>
        </div>
      </b-col>
    </div>
  </div>
</template>
<script>
// @ is an alias to /src

export default {
  name: "HomeView",
  data() {
    return {
      textInput: "",
      listTodo: [],
      id: 0,
    };
  },
  methods: {
    addTodo(textInput) {
      if (textInput !== "") {
        this.listTodo.push({
          id: this.id,
          text: textInput,
          isDone: false,
        });
        this.id++;
        this.textInput = "";
      }
    },
    deleteTodo(item) {
      this.listTodo = this.listTodo.filter((element) => {
        return element.id !== item.id;
      });
    },
  },
};
</script>

<style lang="scss" scoped>
.text-todo {
  background-color: pink;
}
.card-todo {
  width: 70%;
  .display-text {
    text-align: left;
    width: 70%;
    overflow-wrap: break-word;
  }
}
.text-todo-done {
  text-decoration-line: line-through;
}
</style>
