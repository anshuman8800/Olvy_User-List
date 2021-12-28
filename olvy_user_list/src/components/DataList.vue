<template>
  <!-- Main Body is divided into 2 part 
  1st one : if show_search is true : Display the query result 
  2nd one : if show_search is false: Show the Full list -->
  <div id="main_body">
    <!-- Show search result -->
    <div id="search_result" v-if="this.show_search">
      <h4 id="search_heading">
        Search related to
        <span style="color: #ff3a7c"
          ><q>{{ this.searched_data }}</q>
        </span>
        <span>
          <span id="crossbtn">
            <button id="crossBtn" @click="pressOnCrossBtn">X</button>
          </span>
        </span>
      </h4>
      <!-- If table is NOT EMPTY -->
      <b-table
        v-if="this.objects.length"
        striped
        hover
        :items="objects"
      ></b-table>
      <!-- If table is EMPTY -->
      <div v-else>
        <h4 id="nothingFound">OPPS! Nothing Found Here</h4>
      </div>
    </div>
    <!-- Show search result END -->

    <!-- Show full List -->
    <div id="full_list" v-if="!this.show_search">
      <b-table striped hover :items="this.data_list"></b-table>

      <!-- Div tag to handle Infinite Scrolling  -->
      <!-- If this Div tag is visible then Fetch() Method will invoke -->
      <div
        id="scroll_handler"
        v-if="this.data_list.length"
        v-observe-visibility="handleScrolledToBottom"
      >
        <!-- Loading style Animation -->
        <div v-if="this.current_index <= this.MAX_FILE_SIZE">
          <b-spinner id="spinnerV" type="grow" small></b-spinner>
          <b-spinner id="spinnerP" type="grow" small></b-spinner>
          <b-spinner id="spinnerV" type="grow" small></b-spinner>
          <b-spinner id="spinnerP" type="grow" small></b-spinner>
        </div>
      </div>
    </div>
    <!-- Show full List END -->
  </div>
</template>

<script>
import testData from "../assets/user_data_20k.json";
export default {
  name: "DataList",
  computed: {
    // Created Object to show the search result
    objects() {
      let data = [];
      // If show_search is TRUE and search query is numeric i.e. Search by ID
      if (this.show_search && testData.objects[this.searched_data - 1]) {
        data.push(testData.objects[this.searched_data - 1]);
      }
      // If still show_search is ture, i.e. It is Seach by UserName
      else if (this.show_search) {
        for (var i = 0; i < testData.objects.length; i++) {
          if (testData.objects[i]["FirstNameLastName"] == this.searched_data) {
            data.push(testData.objects[i]);
          }
        }
      }
      // return final data List
      return data;
    },
  },
  methods: {
    // FetchObject() : Fetch more 50 object from main source and add it to data list
    async fetchObjects() {
      let end = this.current_index + this.MAX_STEP_SIZE; // MAX_STEP_SIZE = 50 (by default but we can change it)
      // For loop is to push object from current index to end index
      for (
        let start = this.current_index;
        start < end && start < testData.objects.length;
        start++
      ) {
        this.data_list.push(testData.objects[start]);
      }
      // Update the current index
      this.current_index = this.current_index + this.MAX_STEP_SIZE;
      // Set MAX_FILE_SIZE = No of objects = MAX OBJECTS IN Source
      this.MAX_FILE_SIZE = testData.objects.length;
    },
    handleScrolledToBottom(isVisible) {
      // If Div tag with ID="scroll_handler" is visible then invoke fetchObject else return nothing
      if (!isVisible || this.current_index >= this.MAX_FILE_SIZE) {
        return;
      }
      this.fetchObjects();
    },
    pressOnCrossBtn() {
      // set show_result to be false
      this.show_search = false;
    },
  },
  mounted() {
    this.fetchObjects();
  },
  data() {
    return {
      data_list: [], // Objects store in this data_list, Initially Empty
      current_index: 0, // Current index of data_list
      MAX_STEP_SIZE: 50, // Add more 50(MAX_STEP_SIZE) object when fetch function invoke
      MAX_FILE_SIZE: 1, // Maximum no of object in Main source, It will change when 1st time fetch function invoke
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
#search_heading {
  padding-bottom: 1rem;
  color: navy;
  float: center;
}
#nothingFound {
  padding-top: 5rem;
  color: navy;
}
#crossBtn {
  font-weight: bold;
  color: navy;
  border-radius: 28px !important;
  background-color: rgba(0, 0, 0, 0);
  float: right;
}
#crossbtn {
  text-align: right;
}
#spinnerP {
  color: #ff3a7c;
}
#spinnerV {
  color: navy;
}
</style>