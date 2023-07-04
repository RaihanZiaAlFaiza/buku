<template>
  <div class="card-title">
    <div class="text">
      <h3>Form Peminjaman Buku</h3>
      <form @submit.prevent="submitPeminjaman">
        <div class="form-group">
          <label for="idPeminjaman">ID Peminjaman</label>
          <input type="text" class="form-control" v-model="pengembalian.idPeminjaman" id="idPeminjaman" required />
        </div>
        <div class="form-group">
          <label for="tanggal">Tanggal Peminjaman</label>
          <input type="date" class="form-control" v-model="peminjaman.tanggal" id="tanggal" required />
        </div>
        <div class="form-group">
          <label for="tanggal">Tanggal Pengembalian</label>
          <input type="date" class="form-control" v-model="pengembalian.tanggal" id="tanggal" required />
        </div>

        <div class="form-group">
          <label for="nomorAnggota">Nomor Anggota</label>
          <input type="text" class="form-control" v-model="peminjaman.nomorAnggota" id="nomorAnggota" required />
        </div>
        <div class="form-group">
          <label for="kodeBuku">Kode Buku</label>
          <input type="text" class="form-control" v-model="peminjaman.kodeBuku" id="kodeBuku" required />
        </div>
        <button type="submit" class="btn btn-primary">Submit</button>
      </form>
      <h3>Form Pengembalian Buku</h3>
      <form @submit.prevent="submitPengembalian">
        <div class="form-group">
          <label for="idPeminjaman">ID Peminjaman</label>
          <input type="text" class="form-control" v-model="pengembalian.idPeminjaman" id="idPeminjaman" required />
        </div>
        <div class="form-group">
          <label for="tanggal">Tanggal Pengembalian</label>
          <input type="date" class="form-control" v-model="pengembalian.tanggal" id="tanggal" required />
        </div>
        <button type="submit" class="btn btn-primary">Submit</button>
      </form>
    </div>
    <h1>List Peminjaman Buku Yang Masih Dipinjam</h1>
    <table class="table">
      <thead>
        <tr class="table-primary">
          <th>ID</th>
          <th>Tanggal Peminjaman</th>
          <th>Nomor Anggota</th>
          <th>Status Peminjaman</th>
          <th>Tanggal Pengembalian</th>
          <th>Durasi Keterlambatan</th>
        </tr>
      </thead>
      <tbody class="table-secondary">
        <tr v-for="peminjaman in peminjamanDipinjam" :key="peminjaman.id">
          <td>{{ peminjaman.id }}</td>
          <td>{{ peminjaman.tanggal_peminjaman }}</td>
          <td>{{ peminjaman.nomor_anggota }}</td>
          <td>{{ peminjaman.status_peminjaman }}</td>
          <td>{{ peminjaman.tanggal_pengembalian }}</td>
          <td>{{ peminjaman.durasi_keterlambatan }}</td>
        </tr>
      </tbody>
    </table>

    <h1>List Peminjaman Buku Yang Sudah Dikembalikan</h1>
    <table class="table">
      <thead>
        <tr class="table-primary">
          <th>ID</th>
          <th>Tanggal Peminjaman</th>
          <th>Nomor Anggota</th>
          <th>Status Peminjaman</th>
          <th>Tanggal Pengembalian</th>
          <th>Durasi Keterlambatan</th>
        </tr>
      </thead>
      <tbody class="table-secondary">
        <tr v-for="peminjaman in peminjamanDikembalikan" :key="peminjaman.id">
          <td>{{ peminjaman.id }}</td>
          <td>{{ peminjaman.tanggal_peminjaman }}</td>
          <td>{{ peminjaman.nomor_anggota }}</td>
          <td>{{ peminjaman.status_peminjaman }}</td>
          <td>{{ peminjaman.tanggal_pengembalian }}</td>
          <td>{{ peminjaman.durasi_keterlambatan }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      peminjaman: {
        tanggal: "",
        nomorAnggota: "",
        kodeBuku: "",
      },
      pengembalian: {
        idPeminjaman: "",
        tanggalPengembalian: "",
      },
      peminjamanDipinjam: [],
      peminjamanDikembalikan: [],
    };
  },
  mounted() {
    // Mengambil data peminjaman dengan status DIPINJAM dari API backend PHP
    this.fetchPeminjamanDipinjam();
    // Mengambil data peminjaman dengan status DIKEMBALIKAN dari API backend PHP
    this.fetchPeminjamanDikembalikan();
  },
  methods: {
    submitPeminjaman() {
      fetch("https://mhdrmaulana.my.id/buku/peminjamanbuku.php", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(this.peminjaman),
      })
        .then((response) => response.json())
        .then((data) => {
          console.log(data);
          // Lakukan tindakan setelah peminjaman berhasil disimpan
        })
        .catch((error) => {
          console.error(error);
          // Lakukan tindakan jika terjadi kesalahan saat melakukan peminjaman
        });
    },
    submitPengembalian() {
      fetch("https://mhdrmaulana.my.id/buku/pengembalianbuku.php", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(this.pengembalian),
      })
        .then((response) => response.json())
        .then((data) => {
          console.log(data);
          // Lakukan tindakan setelah pengembalian berhasil disimpan
        })
        .catch((error) => {
          console.error(error);
          // Lakukan tindakan jika terjadi kesalahan saat melakukan pengembalian
        });
    },
    fetchPeminjamanDipinjam() {
      // Panggil API backend PHP untuk mendapatkan data peminjaman dengan status DIPINJAM
      axios
        .get("https://mhdrmaulana.my.id/buku/listdipinjam.php")
        .then((response) => {
          this.peminjamanDipinjam = response.data;
        })
        .catch((error) => {
          console.error(error);
        });
    },
    fetchPeminjamanDikembalikan() {
      // Panggil API backend PHP untuk mendapatkan data peminjaman dengan status DIKEMBALIKAN
      axios
        .get("https://mhdrmaulana.my.id/buku/listdikembalikan.php")
        .then((response) => {
          this.peminjamanDikembalikan = response.data;
        })
        .catch((error) => {
          console.error(error);
        });
    },
  },
};
</script>

<style>
.card-title {
  font-family: "Berlin Sans FB Demi";
}
</style>
