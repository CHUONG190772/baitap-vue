<template>
  <div>
    <h2>Thêm sinh viên</h2>
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
      students: [ { maSV: 'SV001', tenSV: 'Nguyễn Văn A', NgaySinh: '01/01/2000', GioiTinh: 'Nam', MaKhoa: 'K001' },
                  { maSV: 'SV002', tenSV: 'Trần Thị B', NgaySinh: '02/02/2001', GioiTinh: 'Nữ', MaKhoa: 'K002' }, { maSV: 'SV003', tenSV: 'Pham Văn C', NgaySinh: '11/10/2000', GioiTinh: 'Nam', MaKhoa: 'K003' },
        { maSV: 'SV004', tenSV: 'Vu Thị D', NgaySinh: '2/02/2001', GioiTinh: 'Nữ', MaKhoa: 'K004' },],
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
