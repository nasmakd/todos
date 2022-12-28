<template>
	<div>
		<TransitionGroup name="list" tag="ul">
			<!-- vue 2.2.0 이상에서는 key 값 필수 propsdata로 바꿈-->
			<li class="shadow" v-for="(todoItem, index) in propsdata" :key="index">
				<i class="fa-regular fa-square-check checkBtn"></i>
				<span class="text">{{ todoItem }}</span>
				<span class="removeBtn" @click="removeTodo(todoItem, index)"
					><i class="fa-solid fa-trash-can"></i
				></span>
			</li>
		</TransitionGroup>
	</div>
</template>

<script>
export default {
	props: ['propsdata'],
	/* App.vue로 이동
  data() {
		return { todoItems: [] };
	}, //storage 내용을 집어넣을 배열 선언
  */
	/** App.vue로 이동
	created: function () {
		if (localStorage.length > 0) {
			for (let i = 0; i < localStorage.length; i++) {
				this.todoItems.push(localStorage.key(i));
			}
		}
	},
*/
	methods: {
		removeTodo: function (todoItem, index) {
			// console.log('value : '+todoItem+', key '+index)

			this.$emit('removeTodo', todoItem, index);
			/** App.vue로 가져감
      localStorage.removeItem(todoItem) // localStorage에서 삭제  
      this.todoItems.splice(index, 1)
      */
			//splice() - 배열에서 특정 항목을 제거
		},
	},
};
</script>

<style scoped>
ul {
	list-style: none;
	min-height: 200px;
}
li {
	display: flex;
	align-items: center;
	background-color: #ebf0d6;
	height: 50px;
	line-height: 50px;
	margin: 18px 0;
	padding-left: 20px;
	border-radius: 6px;
	text-align: left;
}
.checkBtn {
	margin-right: 10px;
	color: #b1b895;
}
.text {
	white-space: nowrap;
	overflow: hidden;
	text-overflow: ellipsis; /* 말줄임표 적용 */
}
.removeBtn {
	margin-left: auto;
	width: 50px;
	text-align: center;
	cursor: pointer;
	color: #3c6255;
}

.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}
.list-enter,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}


</style>
