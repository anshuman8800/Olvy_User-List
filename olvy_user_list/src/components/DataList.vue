<template>
  <div id="main_body">
    <div id="search_result" v-if="this.show_search">
      <h1>Search related to {{ this.searched_data }}</h1>
      <b-table striped hover :items="objects"></b-table>
    </div>
    <div id="full_list" v-if="!this.show_search" >
      <b-table striped hover :items="this.data_list"></b-table>

      <div id="scroll_handler" v-if="this.data_list.length" v-observe-visibility="handleScrolledToBottom" >
        <div v-if="this.current_index <= this.MAX_FILE_SIZE">
          <b-spinner id="spinnerV" type="grow" small></b-spinner>
          <b-spinner id="spinnerP" type="grow" small></b-spinner>
          <b-spinner id="spinnerV" type="grow" small></b-spinner>
          <b-spinner id="spinnerP" type="grow" small></b-spinner>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// import testData from "../assets/testData.json";
// import testData from "../assets/sample_data.json";
import testData from "../assets/user_data_20k.json";
export default {
  name: "DataList",
  computed: {
    objects() {
      let data = [];
      if (this.show_search && testData.objects[this.searched_data - 1]) {
        //For ID
        data.push(testData.objects[this.searched_data - 1]);
      } else if (this.show_search) {
        // For Name
        for (var i = 0; i < testData.objects.length; i++) {
          if (testData.objects[i]['FirstNameLastName'] == this.searched_data) {
            data.push(testData.objects[i]);
          }
        }
      }
      return data;
    },
  },
  methods: {
    async fetchObjects() {
      let end = this.current_index + this.MAX_STEP_SIZE;
      for (
        let start = this.current_index;
        start < end && start < testData.objects.length;
        start++
      ) {
        this.data_list.push(testData.objects[start]);
      }
      this.current_index = this.current_index + this.MAX_STEP_SIZE;
      this.MAX_FILE_SIZE = testData.objects.length; // Set MAX_FILE_SIZE = No of objects
    },
    handleScrolledToBottom(isVisible) {
      if (!isVisible || this.current_index >= this.MAX_FILE_SIZE) {
        return;
      }
      this.fetchObjects();
    },
  },
  mounted() {
    this.fetchObjects();
  },
  data() {
    return {
      current_index: 0,
      MAX_STEP_SIZE: 50,
      data_list: [],
      MAX_FILE_SIZE: 1,
    };
  },
  props: {
    searched_data: String,
    show_search: Boolean,
  },
};
</script>

<style scoped>
#full_list {
  padding-left: 5rem;
  padding-right: 5rem;
}
#search_result {
  padding-left: 5rem;
  padding-right: 5rem;
}
#spinnerP {
  color: #ff3a7c;
}
#spinnerV {
  color: navy;
}
</style>