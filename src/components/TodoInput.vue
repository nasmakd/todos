<template>
	<div class="inputBox shadow">
		<input
			type="text"
			placeholder="Type what you have to do"
			v-model="newTodoItem"
			v-on:keyup.enter="addTodo" />
		<span class="addContainer" v-on:click="addTodo">
			<i class="fa-solid fa-plus"></i><span class="sr_only">추가/add</span>
		</span>
		<!-- 모달 팝업 설정 -->
		<AlertModal v-if=showModal>
			<h3 slot="header">알림</h3>
			<span slot="footer">할일을 입력해주세요 <i class="fa-solid fa-square-xmark closeModalBtn" v-on:click="showModal = false"></i></span>
			
		</AlertModal>
	</div>
</template>

<script>
import AlertModal from './common/AlertModal.vue';
export default {
	data() {
		return { newTodoItem: '', showModal: false };
	},
	methods: {
		addTodo() {
			// console.log('입력한 값은', this.newTodoItem);
			// localStorage.setItem(this.newTodoItem, this.newTodoItem)
			// setItem(key, value) - localStorage에 데이터를 추가하는 API

			// 공백도 입력되는 상황을 막아주기 위해
			if (this.newTodoItem !== '') {
				let value = this.newTodoItem && this.newTodoItem.trim();
				//localStorage.setItem(value, value); 직접 저장하지 않게
				this.$emit('addTodo', value); //상위 App.vue에 addTodo, value 전달
				this.clearInput(); // 분리, 단일책임원칙
			}else{
				// input에 아무것도 입력하지 않았을 때 모달 팝업
				this.showModal = true;
			}
		},
		clearInput() {
			// input 박스 입력후 초기화
			this.newTodoItem = '';
		},
	},
	components: {
		AlertModal: AlertModal,
	},
};
</script>

<style scoped>
.inputBox {
	background: #a6bb8d;
	height: 50px;
	line-height: 50px;
	border-radius: 6px;
	overflow: hidden;
}
.inputBox input {
	font-family: 'Pretendard', Helvetica, Arial, sans-serif;
	height: 50px;
	padding: 0 10px;
	background-color: transparent;
	border: none;
	width: calc(100% - 50px);
	outline: none;
	font-size: 0.9rem;
	transition: 0.3s;
	text-align: center;
}
.inputBox input:focus {
	background-color: rgba(255, 255, 255, 0.26);
}
.inputBox input::placeholder {
	color: rgba(239, 239, 239, 0.6);
}
.inputBox .addContainer {
	float: right;
	cursor: pointer;
	color: #fff;
	background-color: #3c6255;
	width: 50px;
}
.closeModalBtn{
	color: #3c6255;
	font-size: 1.2rem;
	margin-left: 10px;
}
</style>
