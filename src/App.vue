<template>
  <div class="d-flex">
  <Sidebar />
    <div class="page-content">
      <router-view/>
    </div>
  </div>
</template>
<script>
import Sidebar from "@/components/Sidebar";

export default {
  components: {
    Sidebar
  }
}
</script>
<style lang="scss">
@font-face {
  font-family: 'Golos';
  src: url('~@/assets/fonts/golos/Golos-Text_Regular.ttf') format('ttf');
  font-weight: 400;
  font-style: normal;
}
@font-face {
  font-family: 'Golos';
  src: url('~@/assets/fonts/golos/Golos-Text_VF.ttf') format('ttf');
  font-weight: 500;
  font-style: normal;
}
@font-face {
  font-family: 'Golos';
  src: url('~@/assets/fonts/golos/Golos-Text_Bold.ttf') format('ttf');
  font-weight: 800;
  font-style: normal;
}
body {
  font-family: Golos;
  padding: 0;
  margin: 0;
}
#app {
  background: #091F52;

  .page-content {
    width: 100%;
    border-top-left-radius: 50px;
    padding: 40px;
    background: #fff;
  }
}



</style>
