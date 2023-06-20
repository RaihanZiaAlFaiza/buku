<script>
import axios from "axios";
import { onMounted, ref } from "vue";

const readData = "http://localhost/buku/selectkategory.php";

export default {
  data() {
    return {
      kategori: ref([]),
    };
  },
  mounted() {
    this.readData();
  },
  methods: {
    readData() {
      axios
        .get(readData)
        .then((resp) => {
          console.log(resp);
          this.kategori = resp.data;
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>
<template>
  <div>
    <li v-for="data in kategori" style="list-style: none">
      <p>{{ data }}</p>
    </li>
  </div>
</template>
