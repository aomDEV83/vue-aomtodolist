<template>
  <div :class="{ container: true}">
    <h2>Todo List</h2>
    <div style="margin-bottom: 20px">
      <input type="text" name="" id="" placeholder="Search..." style="border-color: rgb(252, 165, 4);"
      :class="{ formControl: true }"
      v-model="searchTodo">
    </div>
    <div>
      <input :class="{ formControl: true }" type="text" name="" id="" placeholder="add todo list"
      style="margin-right: 10px; margin-bottom: 30px"
      v-model="textInput"
      @keyup.enter="addTodo">
      <button :class="{ btnAdd: true }" @click="addTodo">Add</button>
      <button style="margin-left: 10px;" :class="{ btnClear: true }" @click="clearList">Clear</button>
    </div>
    <section>
      <div style="color: #ccc; margin-top: 10px;" v-if="list.length <= 0">
        <small><i>"Items have not been added yet."</i></small>
      </div>
      <div
      v-for="(item, i) in list" :key="item.id">
        <div 
        :class="{ itemCard: true, success: item.status === 'success' }"
        v-if="String(item.msg).toLowerCase().replace(/ /g, '').includes(String(searchTodo).toLowerCase().replace(/ /g, ''))">
          <div>
            <p>{{ item.msg }}</p>
            <p style="color: #ccc; font-size: .7rem;">{{ item.doingTime }}</p>
          </div>
          <div style="display: flex;">
            <button
              :class="{ btnDone: true }"
              @click="doneTodo(i)"
              v-if="item.status === 'pending' ">Done
            </button>
            <button style="margin-left: 5px;"
              :class="{ btnDelete: true }"    
              v-else-if="item.status === 'success' "
              @click="deleteTodo(i)">Delete
            </button>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      textInput: "",
      list: [],
      searchTodo: ""
    }
  },
  methods: {
    addTodo() {
      let val = this.textInput;
      if(val.length <= 0) {
        alert("โปรดใส่ข้อความ");
      }
      else {
        console.log(val)
        this.list.push({
          id: new Date().getTime(),
          msg: val,
          doingTime: String(new Date()).substr(0, 24),
          status: "pending"
        })
        this.textInput = "";
      }
    },
    doneTodo(index) {
      this.list[index].status = "success";
    },
    deleteTodo(index) {
      this.list.splice(index, 1);
    },
    clearList() {
      this.list = [];
    }
  }
}
</script>

<style>

@import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Sans+Thai:wght@400&display=swap');

#app {
  font-family: 'IBM Plex Sans Thai', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.container {
  /* background-color: #2c3e50; */
  width: 70%;
  margin: 0 auto;
}

input:focus {
  outline-color: aquamarine;
}

button {
  cursor: pointer;
}

.itemCard {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #fafafa;
  padding: 10px;
  border-radius: 10px;
  margin-top: 10px;
}

.itemCard.success {
  outline: 2px solid rgb(145, 235, 145);
  background-color: rgb(209, 247, 209);
}

.formControl {
  padding: 10px;
  border: 2px solid deepskyblue;
  border-radius: 5px;
}

.btnAdd {
  border: 2px solid deepskyblue;
  border-radius: 5px;
  padding: 10px 20px;
  background-color: deepskyblue;
  color: #fff;
  font-weight: bold;
}

.btnAdd:hover {
  box-shadow: inset 2px 2px 10px 5px rgb(68, 208, 255), 2px 2px 5px rgb(5, 125, 161);
}

.btnClear {
  border: 2px solid rgb(252, 165, 4);
  border-radius: 5px;
  padding: 10px 20px;
  background-color: rgb(252, 165, 4);
  color: #fff;
  font-weight: bold;
}

.btnClear:hover {
  box-shadow: inset 2px 2px 10px 5px rgb(245, 181, 61), 2px 2px 5px rgb(170, 111, 3);
}

.btnDone {
  border: 2px solid limegreen;
  border-radius: 5px;
  padding: 10px 20px;
  background-color: limegreen;
  color: #fff;
  font-weight: bold;
}

.btnDone:hover {
  box-shadow: inset 2px 2px 10px 5px rgb(68, 214, 68), 2px 2px 5px rgb(5, 161, 39);
}

.btnDelete {
  border: 3px solid rgb(240, 35, 35);
  border-radius: 5px;
  padding: 10px 20px;
  background-color: rgb(240, 35, 35);
  color: #fff;
  font-weight: bold;
}

.btnDelete:hover {
  box-shadow: inset 2px 2px 10px 5px rgb(250, 47, 47), 2px 2px 5px rgb(185, 13, 7);
}

</style>
