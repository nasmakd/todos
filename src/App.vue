<template>
	<div id="app">
		<TodoHeader></TodoHeader>
		<TodoInput v-on:addTodo="addTodo"></TodoInput>
		<TodoList v-bind:propsdata="todoItems" @removeTodo="removeItem"></TodoList>
		<!-- v-bind:props속성이름="사위 컴포넌트의 데이터 이름" - 상위에서 하위로 전달 -->
		<TodoFooter v-on:removeAll="clearAll"></TodoFooter>
	</div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue';
import TodoInput from './components/TodoInput.vue';
import TodoList from './components/TodoList.vue';
import TodoFooter from './components/TodoFooter.vue';

export default {
	// name: 'App',
	data() {
		return { todoItems: [] };
	},
	components: {
		TodoHeader: TodoHeader,
		TodoInput: TodoInput,
		TodoList: TodoList,
		TodoFooter: TodoFooter,
	},
	//새로 인식할 때 localStorage에 남아있는 내용으로 배열을 만들어 준다
	created: function () {
		if (localStorage.length > 0) {
			for (let i = 0; i < localStorage.length; i++) {
				this.todoItems.push(localStorage.key(i));
			}
		}
	},
	methods: {
		addTodo(todoItem){
			localStorage.setItem(todoItem, todoItem);
			this.todoItems.push(todoItem);
		},
		clearAll(){
      localStorage.clear();// localStorage에서만 삭제
			this.todoItems = [] //배열 데이터를 비워줌
    },
		removeItem(todoItem, index){
			localStorage.removeItem(todoItem) // localStorage에서 삭제  
      this.todoItems.splice(index, 1)	//배열에서 삭제
		}

	},
};
</script>

<style>
@font-face {
	font-family: 'Pretendard';
	src: url('https://cdn.jsdelivr.net/gh/Project-Noonnu/noonfonts_2107@1.1/Pretendard-Light.woff')
		format('woff');
	font-weight: 300;
	font-style: normal;
}
@font-face {
	font-family: 'KIMM_Bold';
	src: url('https://cdn.jsdelivr.net/gh/projectnoonnu/noonfonts_2212@1.0/KIMM_Bold.woff2')
		format('woff2');
	font-weight: 700;
	font-style: normal;
}
* {
	box-sizing: border-box;
	margin: 0;
	padding: 0;
}
body {
	background-color: #e2eccc;
}
.sr_only {
	position: absolute;
	clip: rect(0 0 0 0);
	width: 1px;
	height: 1px;
	margin: -1px;
	overflow: hidden;
}
.shadow {
	box-shadow: 0 5px 8px rgba(0, 0, 0, 0.15);
}

#app {
	font-family: 'Pretendard', Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	max-width: 600px;
	margin: auto;
	padding: 30px 3vw;
}
</style>
