<template>
  <div class="container">
    <div class = "form_dropdown">
      <h2>Dropdown Alamat</h2>
      <p>Pilih Provinsi, Kota/Kabupaten, dan Kecamatan</p>
      <select class="drop-item" v-model="pilih_provinsi">
          <option value="">-- Pilih Provinsi --</option>
          <option v-for="(index, province) in data_lokasi" :value="province" :key="index">
            {{ province }}
          </option>
      </select>
      <br />
      <select class="drop-item" v-model="pilih_kota" :disabled="kota.length == 0">
          <option value="">-- Pilih Kabupaten / Kota --</option>
          <option v-for="(index, city) in kota" :value="city" :key="index">
            {{ city }}
          </option>
      </select>
      <br />
      <select class="drop-item" v-model="pilih_kecamatan" :disabled="kecamatan.length == 0">
          <option value="">-- Pilih Kecamatan --</option>
          <option v-for="kec in kecamatan" :value="kec" :key="kec">{{ kec }}</option>
      </select>
    </div>
    <div class = "hasil">
      <h3>Alamat Anda</h3>
      <p v-if="pilih_provinsi&&pilih_kota&&pilih_kecamatan">
          Provinsi {{ pilih_provinsi }}, {{ pilih_kota }}, Kecamatan {{ pilih_kecamatan }}
          <br /><br /></p>

    </div>
    <br/>
    <p>Mahes Production</p>
  </div>
</template>

<script>
export default {
  data: () => ({
    kota: [],
    kecamatan: [],
    pilih_provinsi: '',
    pilih_kota: '',
    pilih_kecamatan: '',
    data_lokasi: {
      'Daerah Khusus Ibukota Jakarta': {
        'Kota Jakarta Utara': ['Tanjung Priok', 'Kelapa Gading', 'Penjaringan'],
        'Kota Jakarta Timur': ['Cakung', 'Jatinegara', 'Kramat Jati'],
        'Kota Jakarta Barat': ['Cengkareng', 'Kebon Jeruk', 'Kalideres'],
        'Kota Jakarta Selatan': ['Kebayoran Baru', 'Mampang Prapatan', 'Setiabudi']
      },
      'Jawa Barat': {
        'Kota Bandung': ['Buahbatu', 'Gedebage', 'Sukajadi'],
        'Kota Cirebon': ['Harjamukti', 'Kejaksan', 'Pekalipan'],
        'Kota Bogor': ['Bogor Barat', 'Bogor Selatan', 'Bogor Utara'],
        'Kota Tasikmalaya': ['Cibeureum', 'Cipedes', 'Indihiang']
      },
      'Daerah Istimewa Yogyakarta': {
        'Kota Yogyakarta': ['Gedongtengen', 'Kotagede', 'Pakualaman'],
        'Kabupaten Sleman': ['Kalasan', 'Prambanan', 'Sleman'],
        'Kabupaten Bantul': ['Imogiri', 'Sanden', 'Sewon'],
        'Kabupaten Gunung Kidul': ['Karangmojo', 'Purwosari', 'Wonosari']
      },
      'Jawa Tengah': {
        'Kota Semarang': ['Gunung Pati', 'Candisari', 'Ngaliyan'],
        'Kota Salatiga': ['Argomulyo', 'Sidorejo', 'Sidomukti'],
        'Kabupaten Sragen': ['Kedawung', 'Miri', 'Sambirejo'],
        'Kabupaten Boyolali': ['Andong', 'Karanggede', 'Mojosongo']
      },
      'Jawa Timur': {
        'Kota Blitar': ['Wlingi', 'Gandusari', 'Kanigoro'],
        'Kota Surabaya': ['Gubeng', 'Rungkut', 'Wiyung'],
        'Kota Malang': ['Blimbing', 'Kedungkandang', 'Klojen', 'Lowokwaru', 'Sukun'],
        'Kota Tulungagung': ['Boyolangu', 'Karangrejo', 'Kauman'],
        'Kota Probolinggo': ['Keandemangan', 'Kanigaran', 'Wonoasih']
      },
      'Bali ': {
        'Kabupaten Tabanan': ['Baturiti', 'Pupuan', 'Selemadeg'],
        'Kabupaten Jembaran': ['Melaya', 'Pekutatan', 'Mendoyo'],
        'Kabupaten Buleleng': ['Banjar', 'Busung Biu', 'Sukasada'],
        'Kabupaten Badung': ['Kuta', 'Mengwi', 'Petang']
      }
    }
  }),
  watch: {
    pilih_provinsi () {
      this.kota = []
      this.kecamatan = []
      this.pilih_kota = ''
      this.pilih_kecamatan = ''
      if (this.pilih_provinsi.length > 0) {
        this.kota = this.data_lokasi[this.pilih_provinsi]
      }
    },
    pilih_kota () {
      this.kecamatan = []
      this.pilih_kecamatan = ''
      if (this.pilih_kota.length > 0) {
        this.kecamatan = this.data_lokasi[this.pilih_provinsi][this.pilih_kota]
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  max-width: 700px;
  margin: 0 auto;
}
.form_dropdown {
  padding: 20px;
  width: 700px;
  margin-bottom: 10px;
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  border-radius: 5px;
  text-align: center;
  background-color: #ffffff
}
.hasil {
  width: 700px;
  padding: 20px;
  box-shadow: 0 4px 8px 0 #7c7c78;
  border-radius: 5px;
  text-align: center;
}
.drop-item {
  width: 600px;
  margin: 10px;
  padding: 10px;
}
h2 {
  color: #808080f8;
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif
}
h4{
  color: rgb(185, 167, 0);
  font-family: 'Times New Roman', Times, serif
}
</style>
