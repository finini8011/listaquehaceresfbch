<template>
    <div class="item">
        <input
            type="checkbox"
            @change="updateCheck()"
            :checked="item.completed"
        />
        <span :class="[item.completed ? 'completed' : '', 'itemText']">{{ item.name }}</span>
    </div>
</template>

<script>
export default {
    props: ['item'],
    methods: {
        updateCheck() {
            this.item.completed = !this.item.completed;
            axios.put('api/item/' + this.item.id, {
                item: this.item
            })
            .then(response => {
                if(response.status == 200) {
                    //this.$emit('itemchanged');
                }
            })
            .catch(error => {
                console.log(error);
            })
        }
    }
}
</script>

<style scoped>
    .completed {
        text-decoration: line-through;
        color: #999999;
    }
    .itemText {
        width: 100%;
        margin-left: 20px;
    }
    .item {
        display: flex;
        justify-content: center;
        align-items: center;
    }
</style>