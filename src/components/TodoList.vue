<template>
  <div class="todo-container">
    <!-- 标题 -->
    <h2 class="todo-title">本周待办事项</h2>

    <!-- 待办列表 -->
    <div class="todo-list">
      <div class="todo-item" v-for="(item, index) in todoList" :key="index">
        <span>{{ item }}</span>
        <button class="delete-btn" @click="removeTodo(index)">删除</button>
      </div>
    </div>

    <!-- 添加待办区域 -->
    <div class="add-area">
      <input
        type="text"
        v-model.trim="newTodo"
        placeholder="请输入待办事项..."
        @keyup.enter="addTodo"
        class="todo-input"
      >
      <button class="add-btn" @click="addTodo">添加</button>
    </div>

    <!-- 清空所有按钮 -->
    <button class="clear-all-btn" @click="clearAll">清空所有</button>
  </div>
</template>

<script setup>
import { ref } from 'vue';

// 初始待办数据（与示例图一致）
const todoList = ref(['去图书馆学习', '上羽毛球课', '会议室开会']);
const newTodo = ref('');

// 添加待办
const addTodo = () => {
  if (!newTodo.value.trim()) {
    alert('请输入待办事项！');
    return;
  }
  todoList.value.push(newTodo.value.trim());
  newTodo.value = '';
};

// 删除待办
const removeTodo = (index) => {
  todoList.value.splice(index, 1);
};

// 清空所有
const clearAll = () => {
  if (confirm('确定清空所有待办事项吗？')) {
    todoList.value = [];
  }
};
</script>

<style scoped>
/* 容器样式（灰色背景框） */
.todo-container {
  width: 600px;
  margin: 50px auto;
  padding: 30px;
  background-color: #f5f5f5; /* 浅灰色背景 */
  border-radius: 8px; /* 圆角边框 */
}

/* 标题样式 */
.todo-title {
  text-align: center;
  color: #333; /* 深灰色文字 */
  margin-bottom: 25px;
  font-size: 24px;
  font-weight: 600;
}

/* 待办列表容器 */
.todo-list {
  margin-bottom: 20px;
}

/* 单个待办项（白色背景条） */
.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px 15px;
  background-color: white;
  border-radius: 4px;
  margin-bottom: 10px; /* 项之间的间距 */
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.05); /* 轻微阴影 */
}

.todo-item span {
  color: #333;
  font-size: 16px;
}

/* 红色删除按钮 */
.delete-btn {
  background-color: #dc3545; /* 红色 */
  color: white;
  border: none;
  padding: 6px 12px;
  border-radius: 4px;
  cursor: pointer;
  font-size: 14px;
  transition: background-color 0.2s;
}

.delete-btn:hover {
  background-color: #bb2d3b; /* 加深的红色 */
}

/* 添加区域样式 */
.add-area {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

/* 输入框样式（蓝色边框） */
.todo-input {
  flex: 1; /* 占满剩余宽度 */
  padding: 10px 15px;
  border: 1px solid #0d6efd; /* 蓝色边框 */
  border-radius: 4px;
  font-size: 16px;
  outline: none;
}

.todo-input::placeholder {
  color: #999; /* 占位符灰色 */
}

/* 蓝色添加按钮 */
.add-btn {
  background-color: #0d6efd; /* 蓝色 */
  color: white;
  border: none;
  padding: 0 20px;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
  transition: background-color 0.2s;
}

.add-btn:hover {
  background-color: #0b5ed7; /* 加深的蓝色 */
}

/* 灰色清空按钮 */
.clear-all-btn {
  display: block;
  margin: 0 auto; /* 居中显示 */
  background-color: #6c757d; /* 灰色 */
  color: white;
  border: none;
  padding: 8px 20px;
  border-radius: 4px;
  cursor: pointer;
  font-size: 14px;
  transition: background-color 0.2s;
}

.clear-all-btn:hover {
  background-color: #5c636a; /* 加深的灰色 */
}
</style>