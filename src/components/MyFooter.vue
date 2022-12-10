<!--  -->
<template>
  <div>
    <div class="todo-footer" v-show="total">
		<label>
			<!-- <input type="checkbox" :checked="isAll" @click="checkAll" /> -->
			<input type="checkbox" v-model="isAll"/>
		</label>
        <span>
            <span>已完成{{doneTotal}}</span> / 全部{{total}}
        </span>
		<button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
	</div>
  </div>
</template>

<script>
export default {
  data () {
    return {
    }
  },
  props: ['todos'],
  computed: {
    total() {
        return this.todos.length
    },
    doneTotal() {
       const x = this.todos.reduce((prev, item) => prev + (item.done? 1 : 0),0)
       return x
    },
    isAll: {
        get() {
            return this.doneTotal === this.total && this.total > 0
        },
        set(value) {
            // return this.checkAllTodo(value)
            this.$emit('checkAllTodo',value)
        }
    }
  },
  methods: {
    checkAll(e) {
        this.checkAllTodo(e.target.checked)
    },
    clearAll() {
        this.$emit('clearTodoAll')
    }
  }
}
</script>

<style  scoped>
/*footer*/
.todo-footer {
		height: 40px;
		line-height: 40px;
		padding-left: 6px;
		margin-top: 5px;
	}

	.todo-footer label {
		display: inline-block;
		margin-right: 20px;
		cursor: pointer;
	}

	.todo-footer label input {
		position: relative;
		top: -1px;
		vertical-align: middle;
		margin-right: 5px;
	}

	.todo-footer button {
		float: right;
		margin-top: 5px;
	}
</style>
