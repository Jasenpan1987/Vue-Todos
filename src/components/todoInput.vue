<template>
    <form @submit.prevent="addNewTodo">
        <div class="form-group" id="addNewTodo">
            <label>New Todo</label>
            <input  class="form-control" 
                type="text" required 
                placeHolder="Cannot be empty"
                v-model="newTodo"
            >
        </div>
    </form>
</template>

<script>
    export default {
        data(){
            return {
                newTodo: ''
            }
        },
        methods: {
            addNewTodo(event){
                this.$emit('newTodo', this.newTodo);
                this.newTodo = '';
            }
        }
    }
</script>