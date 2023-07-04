<template>
  <div>
    <h1>Members</h1>
    <div class="search-form">
      <input type="text" v-model="searchQuery" placeholder="Search Member Number" />
      <button @click="searchMembers">Search</button>
    </div>

    <!-- Tampilkan seluruh anggota -->
    <table class="table">
      <thead>
        <tr>
          <th>Number</th>
          <th>Name</th>
          <th>Gender</th>
          <th>Address</th>
          <th>Phone Number</th>
          <th>Registered Date</th>
          <th>Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="anggota in anggotaList" :key="anggota.id">
          <td>{{ anggota.nomor }}</td>
          <td>{{ anggota.nama }}</td>
          <td>{{ anggota.jenis_kelamin }}</td>
          <td>{{ anggota.alamat }}</td>
          <td>{{ anggota.no_hp }}</td>
          <td>{{ anggota.tanggal_terdaftar }}</td>
          <td>
            <button class="btn btn-primary" @click="editAnggota(anggota)">Edit</button>
            <button class="btn btn-danger" @click="hapusAnggota(anggota.nomor)">Hapus</button>
          </td>
        </tr>
      </tbody>
    </table>

    <!-- Form untuk menambah dan mengedit anggota -->

    <div class="card">
      <div class="card-body">
        <h2>{{ mode === "tambah" ? "Add Member" : "Update Member" }}</h2>
        <form @submit.prevent="submitForm">
          <div class="form-group">
            <label for="nomor">Number:</label>
            <input type="text" class="form-control" v-model="anggota.nomor" required />
          </div>
          <div class="form-group">
            <label for="nama">Name:</label>
            <input type="text" class="form-control" v-model="anggota.nama" required />
          </div>
          <div class="form-group">
            <label for="jenis_kelamin">Gender:</label>
            <select class="form-control" v-model="anggota.jenis_kelamin" required>
              <option value="Laki-laki">Laki-laki</option>
              <option value="Perempuan">Perempuan</option>
            </select>
          </div>
          <div class="form-group">
            <label for="alamat">Address:</label>
            <textarea class="form-control" v-model="anggota.alamat" required></textarea>
          </div>
          <div class="form-group">
            <label for="no_hp">Phone Number:</label>
            <input type="text" class="form-control" v-model="anggota.no_hp" required />
          </div>
          <div class="form-group">
            <label for="tanggal_terdaftar">Registered Date:</label>
            <input type="date" class="form-control" v-model="anggota.tanggal_terdaftar" required />
          </div>
          <button type="submit" class="btn btn-primary" @click="submitForm">{{ mode === "tambah" ? "Add" : "Simpan" }}</button>
          <button type="button" class="btn btn-secondary" @click="resetForm">Cancel</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      anggotaList: [], // Daftar anggota
      anggota: {
        nomor: "",
        nama: "",
        jenis_kelamin: "",
        alamat: "",
        no_hp: "",
        tanggal_terdaftar: "",
      },
      mode: "tambah", // Mode form: tambah atau edit
    };
  },
  mounted() {
    // Ambil seluruh anggota saat komponen di-load
    this.getAnggotaList();
  },
  methods: {
    search() {
      const number = this.searchNumber;
      axios
        .get(`https://mhdrmaulana.my.id/buku/selectnoanggota.php${number}`)
        .then((response) => {
          this.searchedMember = response.data;
        })
        .catch((error) => {
          console.error(error);
          this.searchedMember = null;
        });
    },
    // Ambil seluruh anggota dari backend API
    getAnggotaList() {
      axios
        .get("https://mhdrmaulana.my.id/buku/selectanggota.php")
        .then((response) => {
          this.anggotaList = response.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    // Reset form
    resetForm() {
      this.anggota = {
        nomor: "",
        nama: "",
        jenis_kelamin: "",
        alamat: "",
        no_hp: "",
        tanggal_terdaftar: "",
      };
      this.mode = "tambah";
    },
    // Menambah atau mengedit anggota
    submitForm() {
      if (this.mode === "tambah") {
        axios
          .post("https://mhdrmaulana.my.id/buku/insertanggota.php", this.anggota)
          .then((response) => {
            console.log(response.data);
            // Reset form dan ambil seluruh anggota setelah sukses menambahkan anggota
            this.resetForm();
            this.getAnggotaList();
          })
          .catch((error) => {
            console.log(error);
          });
      } else {
        axios
          .put("https://mhdrmaulana.my.id/buku/updateanggota.php" + this.anggota.nomor, this.anggota)
          .then((response) => {
            console.log(response.data);
            // Reset form dan ambil seluruh anggota setelah sukses mengedit anggota
            this.resetForm();
            this.getAnggotaList();
          })
          .catch((error) => {
            console.log(error);
          });
      }
    },
    // Menghapus anggota berdasarkan nomor
    hapusAnggota(nomor) {
      axios
        .delete("https://mhdrmaulana.my.id/buku/deleteanggota.php" + nomor)
        .then((response) => {
          console.log(response.data);
          // Ambil seluruh anggota setelah sukses menghapus anggota
          this.getAnggotaList();
        })
        .catch((error) => {
          console.log(error);
        });
    },
    // Mengisi form dengan data anggota yang akan di-edit
    editAnggota(anggota) {
      this.anggota = { ...anggota };
      this.mode = "edit";
    },
  },
};
</script>

<style scoped>
/* Styling sesuai kebutuhan Anda */
</style>
