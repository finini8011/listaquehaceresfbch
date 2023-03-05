<template>
  <div class="todoListContainer">
    <div class="card" style="width: 450px">
        <img class="card-img-top" src="https://www.pixel.hn/themes/pixelpay/assets/images/logos/pixelpay.svg" alt="Card image cap" />
        <div class="card-body">
            <h5 class="card-title text-center">Lista de Quehaceres</h5>
            <div class="heading">
                <add-item-form v-on:reloadlist="getList()" />
            </div>
            <list-view :items="items" v-on:reloadlist="getList()" />
        </div>
      </div>
  </div>
</template>

<script>
import addItemForm from "./addItemForm.vue";
import listView from "./listView.vue";
export default {
  components: {
    addItemForm,
    listView,
  },
  data: function () {
    return {
      items: [],
    };
  },
  methods: {
    getList() {
      axios
        .get("api/items")
        .then((response) => {
          this.items = response.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
  created() {
    this.getList();
  },
};
</script>
       
<style scoped>
.todoListContainer {
  width: 400px;
  margin: auto;
}

.heading {
  background: #e6e6e6;
  padding: 10px;
}

#title {
  text-align: center;
}
</style>