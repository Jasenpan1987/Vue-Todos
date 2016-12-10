<template>
    <div class="col-md-12">
        <div class="alert" :class="alertType">
            <span class="todo-item-text">{{ todoItem.text }} <small>({{ completedText }})</small></span> 
            <span class="pull-right">
                <button class="btn btn-success pull-right" @click="completeTodo">Completed</button>
                <button class="btn btn-danger pull-right" @click="deleteTodo">Delete</button>
            </span>
        </div>
    </div>
</template>
<script>
    export default {
        data(){
            return {

            }
        },
        props: ['todoItem'],
        computed: {
            alertType(){
                return this.todoItem.completed ? 'alert-success' : 'alert-info';
            },
            completedText(){
                return this.todoItem.completed ? 'Completed' : 'Incompleted';
            }
        },
        methods: {
            completeTodo(){
                this.$emit('completeTodo', this.todoItem.id);
            },
            deleteTodo(){
                this.$emit('deleteTodo', this.todoItem.id);
            }
        }
    }
</script>

<style scoped>
    button {
        margin-left: 17px;
    }
    .todo-item-text {
        font-size: 18px;
        font-weight: 600;
    }
</style>