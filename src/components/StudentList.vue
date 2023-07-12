<template>
  
  <div>
    <table>
      <thead>
          <tr>
            <th>Mã SV</th>
            <th>Tên SV</th>
            <th>Ngày Sinh</th>
            <th>Giới Tính</th>
            <th>Mã Khoa</th>
            <th>Edit</th>
            <th>Del</th>
          </tr>
        </thead>
    <tbody>
      <tr v-for="student in students" :key="student.maSV">
        <!-- {{ student.maSV }} -- {{ student.tenSV }} -- {{ student.NgaySinh }} -- {{ student.GioiTinh }} -- {{ student.MaKhoa }} &ensp;&ensp; -->
        <td> {{ student.maSV }}</td>
        <td>{{ student.tenSV }}</td>
        <td>{{ student.NgaySinh }}</td>
        <td>{{ student.GioiTinh }}</td>
        <td>{{ student.MaKhoa }}</td>
        <td><button @click="editStudent(student)"><i class="fa fa-pencil"></i></button></td>
        <td><button id="delete" @click="deleteStudent(student.maSV)"><i class="fa-sharp fa-solid fa-trash"></i></button></td>
      </tr>
     
    </tbody>
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
      alert('bạn có chắc chắn')
    },
  },
};
</script>
<style >
/* table th,
table td {
    // padding: 8px;
    text-align: left;
    background-color: lightgoldenrodyellow;
} */
table{
  text-align: right ;
}

table th {
    background-color: #c1bebe;
    text-align: left;
}
table td{
  background-color: whitesmoke;
    text-align: left;
}
td{
  text-align: left;
}
td button{
    background-color: #9090f5;
    border-radius: 10px;
    font-size: large;
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
  color: white;
  padding: 5px 10px;
  border: none;
  cursor: pointer;
  display: inline-block;

}

button:hover {
  background-color: rgb(90, 139, 0);
}
#delete{
  background-color:  rgb(145, 30, 30);
}
#dedede:hover{
  background-color: rgb(90, 139, 0);
}
</style>
