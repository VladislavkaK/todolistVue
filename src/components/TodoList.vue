<template>
  <div class="container">
    <header>
      <h1>{{ title }}</h1>
    </header>
    <form class="form">
      <div class="input-group mb-3">
        <input type="text" class="form-control" placeholder="Добавить задачу" id="itemForm">
        <div class="input-group-append">
          <button type="button" class="btn btn-outline-secondary" v-on:click="addItem">Добавить</button>
        </div>
      </div>
    </form>

    <table class="table table-stripped">
      <thead class="thead-dark">
        <tr>
          <th scope="col">Задачи</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in items" :key="index">
          <th scope="row">
            <label v-if="item !== editingItem" @dblclick="editItem(item)">{{ item.text }}</label>
            <input type="text" v-if="item === editingItem" class="form-control lenInput"
                   @keyup.enter="endEdit(item)" @blur="endEdit(item)" v-model="item.text">
            <button type="button" v-on:click="deleteItem(index)" class="btn btn-danger rightMargin">X</button>
            <!-- <button type="button" v-if="item !== editingTask" v-on:click="editTask(item)" class="btn btn-info rightMargin">Edit</button> -->
          </th>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "TodoList",
  data: function () {
    return {
      title: "Лист задач",
      editingItem: {},
      items: [
        { text: "Привет моя первая задача" },
        { text: "Привет моя 2 задача" },
        { text: "Привет моя 3 задача" },
        { text: "Привет моя 4 задача" },
        { text: "Привет моя 5 задача" }
      ]
    }
  },
  methods: {
    addItem: function () {
      let input = document.getElementById("itemForm");

      if (input.value !== '') {
        this.items.push({
          text: input.value
        })
        input.value = "";
      }
    },
    deleteItem: function (index) {
      this.items.splice(index, 1);
    },
    editItem: function (item) {
			this.editingItem = item;
		},
		endEdit: function (item) {
      this.editingItem = {};
			if (item.text.trim() === ""){
				this.deleteItem(item);
			}
				
		},
  }
    
};
</script>

<style>
  .rightMargin {
     float: right;
  }
  .lenInput {
    width: 600px;
  }
</style>