<template>
  <div>
    <table>
    <ul>
      <li v-for="student in students" :key="student.maSV">
        {{ student.maSV }} -- {{ student.tenSV }} -- {{ student.NgaySinh }} -- {{ student.GioiTinh }} -- {{ student.MaKhoa }} &ensp;&ensp;
        
      </li>
      <button @click="editStudent(student)">Sửa</button>
        <button @click="deleteStudent(student.maSV)">Xóa</button>
    </ul>
  </table>
  </div>
</template>

<script>
export default {
  props: {
    students: {
      type: Array,
      default: () => [],
    },
  },
  methods: {
    editStudent(student) {
      this.$emit("edit", student);
    },
    deleteStudent(maSV) {
      this.$emit("delete", maSV);
    },
  },
};
</script>
<style scoped>
ul {
  list-style: none;
  padding: 0;
}

li {
  margin-bottom: 10px;
  background-color: #f5f5f5;
  padding: 10px;
  border-radius: 5px;
  display: flex;
  align-items: center;
}
li.student-item {
  margin-bottom: 10px;
}
.student-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 10px;
}

.student-item {
  background-color: #f0f0f0;
  padding: 10px;
}

.student-info {
  margin-bottom: 10px;
}

.student-maSV {
  font-weight: bold;
}

.student-actions {
  display: flex;
  justify-content: flex-end;
}

button {
  background-color: blue;
  color: white;
  padding: 5px 10px;
  border: none;
  cursor: pointer;
  display: inline-block;

}

button:hover {
  background-color: rgb(90, 139, 0);
}
</style>
