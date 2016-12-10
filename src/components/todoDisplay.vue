<template>
    <div class="col-md-12 display-bar">
        <span class="label label-default" @click="changeShowItem('all')">Show All</span>
        <span class="label label-primary" @click="changeShowItem('incompleted')">Show Incompleted</span>
        <span class="label label-success" @click="changeShowItem('completed')">Show Completed</span>
    </div>
</template>
<script>
    export default {
        data(){
            return {
                show: 'all'
            }
        },
        methods: {
            changeShowItem(newShow){
                this.show = newShow;
                this.$emit('changeShow', this.show);
            }
        }
    }
</script>
<style scoped>
    .label {
        cursor: pointer;
    }
    .display-bar {
        margin-bottom: 15px;
    }
</style>