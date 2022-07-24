<template>
	<div class="inputBox shadow">
		<input type="text" v-model="newTodoItem" @keypress.enter="addTodo()" />
		<span class="addContainer" @click="addTodo">
			<i class="fa-solid fa-plus addBtn"></i>
		</span>
		<ModalView v-if="showModal">
			<h3 slot="header">
				경고!
				<i class="closeModalBtn fas fa-times" @click="showModal = false"></i>
			</h3>
			<div slot="body">무언가를 입력하세요.</div>
		</ModalView>
		<ModalView v-if="showDuplicate">
			<h3 slot="header">
				중복!
				<i
					class="closeModalBtn fas fa-times"
					@click="showDuplicate = false"
				></i>
			</h3>
			<div slot="body">
				이미 리스트에 있는 내용입니다. 중복되지 않은 값을 입력하세요.
			</div>
		</ModalView>
	</div>
</template>
<script>
import ModalView from './common/ModalView.vue';
import { mapGetters } from 'vuex';
export default {
	data: function () {
		return {
			newTodoItem: '',
			showModal: false,
			showDuplicate: false,
		};
	},
	computed: {
		...mapGetters({
			todoItems: 'storedTodoItems',
		}),
	},
	components: {
		ModalView: ModalView,
	},
	methods: {
		addTodo: function () {
			const nowTodoItems = this.todoItems;

			let checkDuplicate = false;
			nowTodoItems.forEach((cur) => {
				if (cur.item === this.newTodoItem) {
					checkDuplicate = true;
				}
			});

			if (this.newTodoItem !== '' && !checkDuplicate) {
				this.$store.commit('addOneItem', this.newTodoItem);
				this.clearInput();
			} else if (checkDuplicate) {
				this.showDuplicate = !this.showDuplicate;
			} else {
				this.showModal = !this.showModal;
			}
		},
		clearInput: function () {
			this.newTodoItem = '';
		},
	},
};
</script>
<style scoped>
input:focus {
	outline: none;
}
.inputBox {
	background: white;
	height: 50px;
	line-height: 50px;
	border-radius: 5px;
}
.inputBox input {
	height: 40px;
	width: 80%;
	border-style: none;
	font-size: 0.9rem;
}
.addContainer {
	float: right;
	background: linear-gradient(to right, #6478fb, #8763fb);
	display: block;
	width: 3rem;
	border-radius: 0 5px 5px 0;
}
.addBtn {
	color: white;
	width: 50px;
	vertical-align: middle;
}
</style>
