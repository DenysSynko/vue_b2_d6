<script setup>
import { onMounted, ref } from 'vue';
import axios from 'axios';
const students = ref([]);
onMounted(() => {
  axios.get("http://34.82.81.113:3000/students")
    .then((response) => {
      students.value = response.data;
      console.log(response.data); 
    })
    .catch((error) => {
      console.error(error); 
    });
});
</script>

<template>
  <div>
    <table class="w-full border-2 text-left bg-slate-300">
      <thead class="border-b">
        <tr>
          <th>ПІБ</th>
          <th>Група</th>
          <th>Оцінка</th>
          <th>Практика</th>
        </tr>
      </thead>
      <tbody class="bg-slate-200">
        <tr
          v-for="student in students"
          :key="student._id"
        >
          <td>{{ student.name }}</td>
          <td>{{ student.group }}</td>
          <td>{{ student.mark }}</td>
          <td>
            <input type="checkbox" v-model="student.isDonePr" />
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
