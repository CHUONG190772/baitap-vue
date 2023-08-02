<template>
  <div>
    <h2 style = " font-size: xx-large;">Thêm sinh viên</h2>
    <StudentForm 
    @add="addStudent" 
    :editedStudent="editedStudent"
    @update="updateStudent"/>

    <h2>Danh sách sinh viên</h2>
    <StudentSearch @search="searchStudent" />
    <StudentList
      :students="filteredStudents"
      @edit="editStudent"
      @delete="deleteStudent"
    />

  </div>
</template>

<script>
import StudentSearch from "./components/StudentSearch.vue";
import StudentList from "./components/StudentList.vue";
import StudentForm from "./components/StudentForm.vue";

export default {
  components: {
    StudentSearch,
    StudentList,
    StudentForm,
  },
  data() {
    return {
      students: [ { maSV: 'SV001', tenSV: 'Nguyễn Văn A', NgaySinh: '2000-01-01', GioiTinh: 'Nam', MaKhoa: 'CNTT' },
                  { maSV: 'SV002', tenSV: 'Trần Thị B', NgaySinh: '2000-03-05', GioiTinh: 'Nữ', MaKhoa: 'Marketing' }, { maSV: 'SV003', tenSV: 'Phạm Văn C', NgaySinh: '2000-11-01', GioiTinh: 'Nam', MaKhoa: 'Business' },
        { maSV: 'SV004', tenSV: 'Vũ Thị D', NgaySinh: '2000-01-06', GioiTinh: 'Nữ', MaKhoa: 'CNTT' },],
      editedStudent: null,
      searchQuery: "",
      //seletedStudent: null,
    };
  },
  computed: {
    filteredStudents() {
      const query = this.searchQuery.toLowerCase().trim();
      if (query === "") {
        return this.students;
      } else {
      return this.students.filter(student =>
        (student.tenSV && student.tenSV.toLowerCase().includes(query)) ||
        (student.maSV && student.maSV.toLowerCase().includes(query)) ||
        (student.NgaySinh && student.NgaySinh.toLowerCase().includes(query))||
        (student.GioiTinh && student.GioiTinh.toLowerCase().includes(query))||
        (student.MaKhoa && student.MaKhoa.toLowerCase().includes(query))
      );
    }
    },
  },
  methods: {
    addStudent(student) {
      this.students.push(student);
    },
    updateStudent(updatedStudent) {
      const index = this.students.findIndex(
        (student) => student.maSV === updatedStudent.maSV
      );
      if (index !== -1) {
        this.students.splice(index, 1, updatedStudent);
      }
      this.editedStudent = null;
    },
    editStudent(student) {
      this.editedStudent = {...student};
      //this.selectedStudent = {...student};
    },
    deleteStudent(maSV) {
      this.students = this.students.filter(
        (student) => student.maSV !== maSV
      );
    },
    searchStudent(query) {
      this.searchQuery = query;
    },
  },
};
</script>
<style scoped>
body{
  background-color: wheat ;
}
</style>
