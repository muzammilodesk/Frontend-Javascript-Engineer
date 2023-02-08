
<template>
  <div>
    <h2>To do: ({{ todos.length }})</h2>
    <input v-on:keyup.enter="onEnter" v-model="inputData" type="text" placeholder="Type something and press ENTER" />
    <draggable class="dragArea list-group w-full" :list="todos" @change="log">
      <li v-for="(item, index) in todos" v-bind:key="item.text">
        <label>
          <input v-model="item.isCompleted" @change="handleCheck(index)" type="checkbox" />
          <span>{{ item.text }}</span>
          <a @click="onRemoveTodo(index)" class="remove">Remove</a>
        </label>
      </li>
    </draggable>

    <hr />
    <h2>
      Completed items: ({{ completed }})
    </h2>
  </div>
</template>


<script>

import { VueDraggableNext } from 'vue-draggable-next'
export default {
  components: {
    draggable: VueDraggableNext,
  },
  data() {
    return {
      completed: 0,
      enabled: true,
      dragging: false,
      todos: [
        { text: "Learn about Vue", isCompleted: false },
        { text: "Learn about Fliplet", isCompleted: false },
        { text: "Play around in JSFiddle", isCompleted: false },
        { text: "Show us what you've got", isCompleted: false }
      ]
    }
  },
  methods: {
    onEnter: function () {
      if (this.inputData == '')
        return
      this.todos.push({ text: this.inputData })
      this.inputData = ''
    },

    onRemoveTodo(index) {
      if (this.todos[index].isCompleted)
        this.completed = this.completed - 1
      this.todos.splice(index, 1);
      this.completed = temp
    },

    handleCheck(index) {
      let comp = 0
      this.todos.map((ele, i) => {
        if (ele.isCompleted)
          comp++
        if (i == index)
          return { ...ele, ['isCompleted']: !ele.isCompleted }
        return ele
      })
      this.todos.sort((x, y) => (x.isCompleted === y.isCompleted) ? 0 : x.isCompleted ? -1 : 1)
      console.log("check sorting ", comp)
      this.completed = comp
    },
    log(ele) {
      // console.log("check sorting ",ele)
    },
  }
}
</script>



<style scoped>
li {
  margin: 8px 0;
}

h2 {
  font-weight: bold;
  margin-bottom: 15px;
}

del {
  color: rgba(0, 0, 0, 0.3);
}

input[type="text"] {
  padding: 10px;
  width: 200px;
}

label .remove {
  display: none;
  color: red;
}

label:hover .remove {
  display: inline-block;
  margin-left: 10px;
  color: red;
  opacity: 0.5;
}
</style>
