<template>
  <div id="app">
    <div class="title">
      <h1>タスク一覧</h1>
    </div>
    <div id="main">
      <div class="tasks-display">
        <div class="tasks">
          <table>
            <tr v-for="(list, index) in lists" v-bind:key="index">
              <td id="todo-item">{{ list.todoItem }}</td>
              <td>
                <button @click="deleteTask(list.id)" id="complete-button">
                  完了
                </button>
              </td>
            </tr>
          </table>
        </div>
      </div>
      <div class="input-form">
        <form @submit.prevent>
          <input
            type="text"
            v-model="todoItem"
            id="todo-input"
            placeholder="タスクフォーム"
          />
          <input type="submit" value="追加" @click="addTask" id="add-button" />
        </form>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";

export default defineComponent({
  data() {
    return {
      lists: [],
      todoItem: "",
    };
  },
  methods: {
    addTask: function () {
      const todo = {
        id: this.lists.length,
        todoItem: this.todoItem,
      };
      if (this.todoItem == "") {
        window.alert("タスクの入力は必須です。");
      } else {
        (this as any).lists.push(todo);
      }
      this.todoItem = "";
    },
    deleteTask(list_id: number) {
      if (list_id > -1) {
        this.lists.splice(list_id, 1);
        this.lists.forEach((list: any, index: number) => {
          list.id = index;
        });
      }
    },
  },
});
</script>

<style scoped>
/* * {
  outline: solid 1px #000;
} */
h1 {
  font-size: 20px;
  color: #008080;
}
#main {
  background: #d9f1f1;
  padding: 20px;
  border-radius: 0.5rem;
  width: 70%;
  margin: 0 auto;
}
#todo-input {
  border-radius: 0.2rem;
  border: none;
  padding: 7px 10px;
  font-size: 15px;
}
.tasks {
  display: inline-block;
  text-align: center;
}
#add-button {
  color: #fff;
  background: #2c9c9c;
  border-radius: 0.2rem;
  border: none;
  padding: 5px 10px;
  font-size: 15px;
}
#add-button:hover {
  background: #31afaf;
}
#complete-button {
  color: #fff;
  background: #2c9c9c;
  border-radius: 0.2rem;
  border: none;
  padding: 5px 10px;
  font-size: 15px;
}
#complete-button:hover {
  background: #31afaf;
}
#todo-item {
  color: #2c9c9c;
  font-size: 15px;
  font-weight: bold;
}
</style>
