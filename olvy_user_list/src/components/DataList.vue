<template>
  <div id="root_DataList">
    <div id="data_list">
      <b-table striped hover :items="objects"></b-table>
    </div>
  </div>
</template>

<script>
import testData from "../assets/testData.json";
// import testData from "../assets/sample_data.json";
// import testData from "../assets/user_data_20k.json";
export default {
  name: "DataList",
  computed: {
    objects() {
        let data = [];
        // data.push(testData.objects[16279])
        data = testData.objects;
      return data;
    },
  },
  //   data() {
  //     showData = true;
  //   },
};
</script>

<style scoped>
#data_list {
  padding-left: 6rem;
  padding-right: 6rem;
}
</style>