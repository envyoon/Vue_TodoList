<template>
  <div>
    <ul>
      <li v-for="(todoItem, index) in todoItems" :key="index" class="shadow">
        {{ todoItem.value }}
        <span class="removeBtn" @click="removeTodo(todoItem.key, index)">
          <button>delete</button>
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      todoItems: [],
    };
  },
  methods: {
    removeTodo: function (todoItem, index) {
      this.todoItems.splice(index, 1);
      localStorage.removeItem(todoItem);
    },
  },
  created: function () {
    if (localStorage.length > 0) {
      for (var i = 0; i < localStorage.length; i++) {
        if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
          var key = localStorage.key(i);
          var value = localStorage.getItem(key);
          this.todoItems.push({ key: key, value: value });
        }
      }
    }
    this.$nextTick(() => {
      // 데이터가 변경되었으므로 UI를 강제로 다시 렌더링
    });
  },
};
</script>

<style>
ul {
  list-style-type: none;
  padding-left: 0px;
  margin-top: 0;
  text-align: left;
}
li {
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
}
.checkBtn {
  line-height: 45px;
  color: #62acde;
  margin-right: 5px;
}
.checkBtnCompleted {
  color: #b3adad;
}
.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}
.removeBtn {
  margin-left: auto;
  color: #de4343;
}
</style>
