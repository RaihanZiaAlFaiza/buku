<script>
import axios from "axios";
import { onMounted, ref } from "vue";

const readData = "http://localhost/buku/selectbuku.php";

export default {
  data() {
    return {
      buku: ref([]),
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
          this.buku = resp.data;
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
    <li v-for="data in buku" style="list-style: none">
      <p>{{ data }}</p>
    </li>
  </div>
  
</template>
