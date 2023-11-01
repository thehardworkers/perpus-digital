<template>
  <div>
    <table>
      <thead>
        <tr>
          <th>#</th>
          <th>Nama</th>
          <th>Anggota</th>
          <th>Kelas</th>
          <th>Keperluan</th>
          <th>Tanggal</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in items" :key="item.id">
          <td>{{ item.id }}</td>
          <td>{{ item.nama }}</td>
          <td>{{ item.anggota }}</td>
          <td>{{ item.kelas }}</td>
          <td>{{ item.keperluan }}</td>
          <td>{{ item.tanggal }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";

const supabase = useSupabaseClient();
const items = ref([]);
async function ambilData() {
  let { data, error } = await supabase.from("pengunjung").select();
  if (error) throw error;
  if (data) items.value = data;
}

onMounted(() => {
  ambilData();
  console.log(supabase);
});
</script>

<style lang="scss" scoped></style>
