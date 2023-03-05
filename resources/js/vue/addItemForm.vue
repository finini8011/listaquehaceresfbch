<template>
    <table class="table">
        <tbody>
            <tr>
                <td>
                    <input type="text" v-model="item.name" />
                </td>
                <td>
                    <font-awesome-icon
                        icon="plus-square"
                        @click="addItem()"
                        :class="[ item.name ? 'active' : 'inactive' , 'plus']"
                    />
                </td>
            </tr>
            <tr>
                <td class="text-center">
                    Clic para eliminar todos los registros
                </td>
                <td class="text-left">
                    <button @click="deleteItems()" class="trashcan">
                        <font-awesome-icon
                            icon="trash"
                        />
                    </button>
                </td>
            </tr>
            <tr>
                <td class="text-center">
                    Clic para eliminar solo registros seleccionados
                </td>
                <td class="text-left">
                    <button @click="deleteCheckItems()" class="trashcheckcan">
                        <font-awesome-icon
                            icon="trash"
                        />
                    </button>
                </td>
            </tr>
        </tbody>
    </table>
</template>

<script>
export default {
    data: function () {
        return {
            item: {
                name: ""
            }
        }
    },
    methods: {
        addItem() {
            if(this.item.name == '') {
                return;
            }

            axios.post('api/item/store', {
                item: this.item
            })
            .then(response => {
                if( response.status == 201 ) {
                    this.item.name = "";
                    this.$emit('reloadlist');
                }
            })
            .catch(error => {
                console.log(error);
            })
        },
        deleteItems() {
            axios.delete('api/item/all')
            .then(response => {
                if(response.status == 200) {
                    this.$emit('reloadlist');
                }
            })
            .catch(error => {
                console.log(error);
            })
        },
        deleteCheckItems() {
            axios.delete('api/item/check')
            .then(response => {
                if(response.status == 200) {
                    this.$emit('reloadlist');
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
    .addItem {
        display: flex;
        justify-content: center;
        align-items: center;
    }
    input {
        background: #f7f7f7;
        border: 0px;
        outline: none;
        padding: 5px;
        margin-right: 10px;
        width: 100%;
    }
    .plus {
        font-size: 30px;
        padding: 5px;
    }
    .active {
        color: #00ce25;
    }
    .inactive {
        color: #999999;
    }
    .trashcan {
        background: #ece6e6;
        border: none;
        color: #FF0000;
        outline: none;
        font-size: 20px;
    }
    .trashcheckcan {
        background: #f1e0e0;
        border: none;
        color: #0f8645;
        outline: none;
        font-size: 20px;
    }
</style>