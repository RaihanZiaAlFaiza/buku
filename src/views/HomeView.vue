<template>
  <!--banner image-->

  <div class="banner-image w-100 vh-100 d-flex justify-content-center align-items-center">
    <div class="content text-center">
      <img src="../assets/welcomebg.png" class="img-fluid" />
      <h1 class="text-white">TO REY BOOK STORE!</h1>
    </div>
    <div class="col-lg-4">
      <img src="../assets/bookbg.png" class="img-fluid" />
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {
    // HelloWorld
  },
};
</script>

<style>
.banner-image {
  background: #138fc8;
  font-family: "Times New Roman";
  font-style: italic;
  font-size: 30px;
}
.col-lg-4 {
  margin-top: 40px;
  margin-left: 20px;
}
.col-lg-5 {
  margin-left: -400px;
  margin-bottom: 500px;
}
</style>
