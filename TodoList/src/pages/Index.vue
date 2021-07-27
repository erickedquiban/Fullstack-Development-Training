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

    <q-btn label="Confirm" color="primary" @click="confirm" />
    <div v-if="existingToDo == 0">
      <p>No Data found</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",

framework: {
  plugins: ['Dialog']
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
      if (this.todo == 0) {
        alert("Please Fill up the input box");
      } else {
        this.existingToDo.push(this.todo), (this.todo = "");
        console.log(this.existingToDo);
      }
    },

    deleteToDo(index) {
      this.existingToDo.splice(index, 1);
      alert("Are you sure you want to delete the item?");
    },

    editTodo(index, todo) {
      this.todo = todo;
      this.selectedIndex = index;
      this.isEditing = true;
    },
    confirm () {
      this.$q.dialog({
        dark: true,
        title: 'Confirm',
        message: 'Would you like to turn on the wifi?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        console.log('>>>> OK')
      }).onOk(() => {
        // console.log('>>>> second OK catcher')
      }).onCancel(() => {
        // console.log('>>>> Cancel')
      }).onDismiss(() => {
        // console.log('I am triggered on both OK and Cancel')
      })
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
