<template>
  <div>
    <b-navbar toggleable="lg" type="light">
      <!-- Left Side :: Olvy Logo and Name  -->
      <span id="leftSpace"></span>
      <b-img
        left
        src="olvy_logo.png"
        alt="Left image"
        width="36"
        height="36"
      ></b-img>
      <b-navbar-brand href="#" width="100" height="36" class="font-weight-bold"
        >Olvy</b-navbar-brand
      >
      <!-- Left Side :: Olvy Logo and Name -->

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
      <!-- Main Navigation Bar -->
      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item-dropdown text="Products">
            <b-dropdown-item href="#">In-App Widgets</b-dropdown-item>
            <b-dropdown-item href="#">Widget Demo</b-dropdown-item>
            <b-dropdown-item href="#">Standlone Page</b-dropdown-item>
            <b-dropdown-item href="#">Dashboard</b-dropdown-item>
          </b-nav-item-dropdown>
          <b-nav-item href="#">All Feature</b-nav-item>
          <b-nav-item href="#">Prices</b-nav-item>
          <b-nav-item-dropdown text="Resources">
            <b-dropdown-item href="#">Help Center</b-dropdown-item>
            <b-dropdown-item href="#">Installation Guide</b-dropdown-item>
            <b-dropdown-item href="#">Api Documentation</b-dropdown-item>
            <b-dropdown-item href="#">Release Notes</b-dropdown-item>
          </b-nav-item-dropdown>
          <b-nav-item href="#">Product Updates</b-nav-item>
        </b-navbar-nav>
        <!-- Main Navigation Bar -->

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-nav-form id="searchBar" onsubmit="return false;">
            <!-- Input field -->
            <b-form-input
              size="sm"
              class="mr-sm-2"
              placeholder="Search"
              v-model="value"
              v-on:keyup.enter="search()"
              id="input"
            ></b-form-input>
            <!-- Search button -->
            <b-button
              size="sm"
              class="my-2 my-sm-0"
              v-on:click="search()"
              id="searchBtn"
              >Search</b-button
            >
          </b-nav-form>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: "Header",
  methods: {
    // Search Function : Emit the search data to App component
    // Set showed_result varibale to true and reset input field to null
    search() {
      this.searched_data = this.value;
      this.value = "";

      if (this.searched_data) this.showed_result = true;
      else this.showed_result = false;

      this.$emit("clicked_search", this.searched_data, this.showed_result);
    },
  },
  data() {
    return { value: "", searched_data: "", showed_result: false };
  },
};
</script>

<style scoped>
.navbar-brand {
  font-size: 30px;
  color: navy;
}
#searchBar {
  padding-right: 5rem;
}
#leftSpace {
  padding-left: 5rem;
}
#searchBtn {
  background-color: navy;
  font-size: 1rem;
}
</style>