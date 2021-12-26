<template>
  <div id="root">
    <div>
      <h1 id="heading" class="font-weight-bold">
        Welcome to Olvy
        <span style="color: #ff3a7c"> User</span>
        <span style="color: voilet"> List </span>
        <span>
          <sup>
            <b-spinner
              style="color: #ff3a7c"
              small
              label="Small Spinner"
              type="grow"
            ></b-spinner>
          </sup>
        </span>
      </h1>
    </div>

    <div id="dat_list">
      <DataList :searched_data = "searched_data" :show_search = "show_search"/>
    </div>
  </div>
</template>

<script>
import DataList from "./DataList.vue";

export default {
  name: "Body",
  components: {
    DataList,
  },
  props:{
    searched_data : String,
    show_search : Boolean,
  }
};
</script>

<style scoped>
#heading {
  color: navy;
  padding-top: 3rem;
  padding-bottom: 3rem;
}
#data_list {
  padding-left: 6rem;
  padding-right: 6rem;
}
</style>