<template>
  <div id="app">
    <div class="row">
      <div no-padding class="col-12 offset-md-2 col-md-6">
        <h4>Todo List Crud</h4>
      </div>
    </div>

    <div class="row" v-if="!isEditing">
      <div class="col-8  offset-md-2 col-md-6">
        <q-input outlined v-model="todo" label="Add Item" />
      </div>
      <div class="col-4 col-md-2">
        <q-btn color="primary" @click="add" label="Add" />
      </div>
    </div>

    <div class="row" v-else>
      <div class="col-8  offset-md-2 col-md-6">
        <q-input outlined v-model="todo" label="Edit Item" />
      </div>
      <div class="col-3 col-md-2">
        <q-btn color="primary" @click="updateToDo" label="Submit" />
      </div>
    </div>

    <q-list v-for="(todo, index) in existingToDo" bordered>
      <q-item clickable v-ripple>
        <q-item-section>{{ index + 1 }}. {{ "" + todo }} </q-item-section>
        <q-item-section avatar>
          <q-icon color="primary" @click="deleteToDo(index)" name="delete" />
        </q-item-section>
        <q-item-section avatar>
          <q-icon color="primary" @click="editTodo(index, todo)" name="edit" />
        </q-item-section>
      </q-item>
    </q-list>
    <div v-if="existingToDo == 0">
      <p>No Data found</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",

  framework: {
    plugins: ["Dialog"]
  },

  data() {
    return {
      confirm: false,
      isEditing: false,
      selectedIndex: null,
      todo: "",
      existingToDo: [
        "Todo List",
        "Watch Youtube",
        "Full Stack Development Training",
        "Tokyo Revengers",
        "Shinzou wo Sasageyo!"
      ]
    };
  },

  mounted() {
    console.log(this.existingToDo);
  },

  methods: {
    add() {
     if (confirm('Are you sure you want to add this item?')) {
        this.existingToDo.push(this.todo), (this.todo = "");
      }
    },

    deleteToDo(index) {
      if (confirm("Are you sure you want to delete the item?")) {
        this.existingToDo.splice(index, 1);
      }
    },

    editTodo(index, todo) {
      this.todo = todo;
      this.selectedIndex = index;
      this.isEditing = true;
    },

    updateToDo() {
      this.existingToDo.splice(this.selectedIndex, 1, this.todo);
      this.isEditing = false;
      this.todo = "";
      console.log(this.existingToDo);
    }
  }
};
</script>

<style lang="sass" scoped>
.row > div
  padding: 10px 15px
.row + .row
  margin-top: 1rem
</style>
