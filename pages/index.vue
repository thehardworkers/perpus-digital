<template>
  <div>
    <div class="row justify-content-center">
      <div class="col-lg-4">
        <h2 class="my-3">Isi Buku Kunjungan</h2>
        <form @submit.prevent="handleSubmit">
          <div class="mb-3">
            <input v-model="Nama" type="text" class="form-control" placeholder="Masukan Nama" required />
          </div>
          <div class="mb-3">
            <select v-model="Keanggotaan" class="form-control" name="" id="" required>
              <option value="">Pilih Keanggotaan</option>
              <option value="Guru">Guru</option>
              <option value="Siswa">Siswa</option>
              <option value="Staff">Staff</option>
            </select>
          </div>
          <div v-if="Keanggotaan == 'Siswa'" class="mb-3">
            <input v-model="Kelas" type="text" class="form-control" placeholder="Masukan Kelas" required />
          </div>
          <div class="mb-3">
            <textarea v-model="Keperluan" class="form-control" name="" id="" cols="30" rows="10" placeholder="Tulis Keperluan" required></textarea>
          </div>
          <button type="submit" class="btn btn-primary">Kirim</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient();
const Nama = ref("");
const Keanggotaan = ref("");
const Kelas = ref("");
const Keperluan = ref("");

async function handleSubmit() {
  const { error } = await supabase.from("pengunjung").insert([
    {
      nama: Nama.value,
      anggota: Keanggotaan.value,
      kelas: Kelas.value,
      keperluan: Keperluan.value,
    },
  ]);

  if (!error) navigateTo("/kunjungan");
  else throw error;
}
</script>

<style lang="scss" scoped></style>
