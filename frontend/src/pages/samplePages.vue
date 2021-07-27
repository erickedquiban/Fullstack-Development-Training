// Template  User-Interface

<template>
  <div>
    <!-- CODE -->
    <p>Sample</p>
    <p>Name : {{name}}</p>
    <q-input v-model="name" label="Name" />
       <q-btn @click="buttonAction" color="green" text-color="black" label="Action 1" />
       <q-btn @click="buttonAction2" color="red" text-color="black" label="Action 2" />

    <!-- <input type="text" v-model="name"> 
    <button @click="buttonAction">Action 1 </button>
    <button  @click="buttonAction2">Action 2 </button> -->
  <div padding>
    <div>
     <div class="q-pa-md">
     <div class="q-pa-md">
       <div class="row">
      <div no-padding class="col-12 offset-md-2 col-md-6">
       <h4>Todo List Crud</h4>
      </div>
       </div>

    <div class="row">
      <div class="col-12  offset-md-2 col-md-6">
          <q-input outlined v-model="text" label="Add Item" />
      </div>
      <div class="col-12 col-md-2">
         <q-btn color="primary" label="Add" />
      </div>
    </div>

     <div class="row">
      <div class="col-12  offset-md-1 col-md-3">
      <q-checkbox v-model="right" label="Label on Right" />
      </div>
       <div style="font-size: 2em" class="col-12  offset-md-5  col-md-2 ">
          <!-- <q-btn @click="buttonAction" color="green" text-color="black" label="Delete" />
           -->
           <q-icon name="delete"  @click="btnDelete"/>
      </div>
    </div>
  </div>

  </div>
  </div>
  </div>
  </div>
</template>

// Script Behavior and functionality

<script>
//  LifeHooks
// data bidings
// 1 ways of data binding
// 2 data binding
export default {
  data() {
    return {
      name: "Erick Edquiban",
      age: "28",
      right: true
    };
  },
  methods: {
    buttonAction: function () {
        alert ("Action 1");
    },

    buttonAction2: function () {
        alert ("Action 2");

    },
  },
  mounted() {
    alert (" Hello World ");
  },
};
</script>


// Style 

<style lang="sass" scoped>
.row > div
  padding: 10px 15px
.row + .row
  margin-top: 1rem
</style>