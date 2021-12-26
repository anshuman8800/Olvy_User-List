<template>
  <div id="root_DataList">
    <div id="data_list">
      <h1>Search related to {{ this.searched_data }}</h1>
      <b-table striped hover :items="objects"></b-table>
    </div>
  </div>
</template>

<script>
// import testData from "../assets/testData.json";
import testData from "../assets/sample_data.json";
// import testData from "../assets/user_data_20k.json";
export default {
  name: "DataList",
  computed: {
    objects() {
      let data = [];
      if (this.show_search && testData.objects[this.searched_data - 1]) {
        data.push(testData.objects[this.searched_data - 1]);
      } else {
        // data = testData.objects;
        //part 1
        let start = this.current_index;
        let end = this.current_index+this.MAX_SIZE;
        while(start < end){
          data.push(testData.objects[start]);
          start++;
        }
        // this.current_index = 1;
        window.addEventListener("scroll", ()=>{
          // console.log("hihihi");
          console.log(window.scrollY+'  '+window.innerHeight+'  '+document.documentElement.scrollHeight)
          if(window.scrollY + window.innerHeight +1200 >= document.documentElement.scrollHeight){
            console.log("more image requieed");
            let start = this.current_index;
            let end = this.current_index+this.MAX_SIZE;
            while(start < end){
              data.push(testData.objects[start]);
              start++;
            }
          }
        });


      }
      return data;
    },
  },
  data() {
    return {
      current_index : 0,
      MAX_SIZE : 50,
    };
  },
  props: {
    searched_data: String,
    show_search: Boolean,
  },
};
</script>

<style scoped>
#data_list {
  padding-left: 6rem;
  padding-right: 6rem;
}
</style>