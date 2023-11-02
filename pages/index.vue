<template>
  <div>
    <form @submit.prevent="handleSubmit">
      <div>
        <input v-model="Nama" type="text" placeholder="Masukan Nama" required >
      </div>
      <div>
        <select v-model="Keanggotaan" name="" id=""  required>
          <option value="">Pilih Keanggotaan</option>
          <option value="Guru">Guru</option>
          <option value="Siswa">Siswa</option>
          <option value="Staff">Staff</option>
        </select>
      </div>
      <div v-if="Keanggotaan == 'Siswa'"> 
        <input v-model="Kelas" type="text" placeholder="Masukan Kelas" required>
      </div>
      <div>
        <textarea  v-model="Keperluan" name="" id="" cols="30" rows="10" placeholder="Tulis Keperluan" required></textarea>
      </div>
      <button type="submit">Kirim</button>
    </form>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient()
const Nama = ref("")
const Keanggotaan = ref("")
const Kelas = ref("")
const Keperluan = ref("")

async function handleSubmit(){
  const {error} = await supabase
    .from('pengunjung')
    .insert([{
      nama:Nama.value,
      anggota:Keanggotaan.value,
      kelas:Kelas.value,
      keperluan:Keperluan.value
    }])

    if(!error) navigateTo('/kunjungan')
    else throw error
}
</script>

<style lang="scss" scoped>

</style>
