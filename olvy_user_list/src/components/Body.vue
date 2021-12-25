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
      <DataList />
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