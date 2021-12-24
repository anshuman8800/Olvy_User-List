<template>
  <!-- Footer -->
  <mdb-footer color="black" class="font-small pt-0">
    <div class="footer-copyright text-center py-3">
      <mdb-container fluid>
        &copy; 2021 Olvy Inc. All rights reserved.
      </mdb-container>
    </div>
  </mdb-footer>
  <!-- Footer -->
</template>

<script>
import { mdbFooter, mdbContainer } from "mdbvue";
export default {
  name: "Footer",
  components: {
    mdbFooter,
    mdbContainer,
  },
};
</script>