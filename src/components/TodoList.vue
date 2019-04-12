<template>
  <div class="container">
    <h1 class="container__title">Welcome to your todo list !</h1>

    <h2>TODO:</h2>
    <div v-if="toDoItems.length > 0">
      <div :key="item.id" v-for="item of toDoItems">
        <todo-item
          :handleHighLight="handleHighLight"
          :handleItemClick="handleItemClick"
          :highLight="highLightId === item.id"
          :item="item"
        ></todo-item>
      </div>
    </div>
    <div class="container__no-item" v-else>
      No item to display
    </div>

    <h2>DONE:</h2>
    <div v-if="doneItems.length > 0">
      <div :key="item.id" v-for="item of doneItems">
        <todo-item
          :handleHighLight="handleHighLight"
          :handleItemClick="handleItemClick"
          :highLight="highLightId === item.id"
          :item="item"
        ></todo-item>
      </div>
    </div>
    <div class="container__no-item" v-else>
      No item to display
    </div>

    <h2>ADD TODO:</h2>
    <div class="container__add-todo">
      <label class="container__add-todo__label">Todo name:</label>
      <input class="container__add-todo__input" type="text" v-model="title" />
      <button @click="addTodo" class="container__add-todo__button">
        Add Todo
      </button>
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem";

export default {
  name: "TodoList",
  components: {
    "todo-item": TodoItem
  },
  data() {
    return {
      highLightId: null,
      items: [
        {
          id: 0,
          title: "Build vue components",
          state: "TODO"
        },
        {
          id: 1,
          title: "Build your stories",
          state: "TODO"
        },
        {
          id: 2,
          title: "Profit",
          state: "TODO"
        }
      ],
      title: ""
    };
  },
  computed: {
    toDoItems() {
      return this.items.filter(i => i.state === "TODO");
    },
    doneItems() {
      return this.items.filter(i => i.state === "DONE");
    }
  },
  methods: {
    addTodo() {
      if (this.title.length === 0) {
        return;
      }

      this.items.push({
        id: this.items.length,
        title: this.title,
        state: "TODO"
      });
      this.title = "";
    },
    handleHighLight(itemId) {
      if (itemId === this.highLightId) {
        this.highLightId = null;
        return;
      }

      this.highLightId = itemId;
    },
    handleItemClick(itemId) {
      const currentState = this.items[itemId].state;

      // Reset highlight if this highlighted item is done.
      if (itemId === this.highLightId && currentState === "TODO") {
        this.highLightId = null;
      }

      // Toggle item.
      this.items[itemId].state = currentState === "TODO" ? "DONE" : "TODO";
    }
  }
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
}

.container__title {
  align-self: center;
  margin-bottom: 20px;
}

.container__no-item {
  align-self: center;
  font-style: italic;
}

.container__add-todo {
  margin-top: 15px;
  display: flex;
  justify-content: center;
}

.container__add-todo__label {
  margin-right: 5px;
}

.container__add-todo__input {
  margin-right: 25px;
}
</style>
