<template>
  <div>
    <input type="text" v-model="maSV" placeholder="Mã sinh viên" />
    <br>
    <input type="text" v-model="tenSV" placeholder="Tên sinh viên" />
    <br>
    <input type="text" v-model="NgaySinh" placeholder="Ngày Sinh" />
    <br>
    <input type="text" v-model="GioiTinh" placeholder="Giới tính" />
    <br>
    <input type="text" v-model="MaKhoa" placeholder="Mã Khoa" />
    <br>
    <button @click="addStudent">Thêm sinh viên</button>
    <button v-if="editedStudent" @click="updateStudent">Cập nhật sinh viên</button>
  </div>
</template>

<script>
export default {
  props: {
    editedStudent: {
      type: Object,
      default: null,
    },
  },
  data() {
    return {
      maSV: "",
      tenSV: "",
      NgaySinh: "",
      GioiTinh:"",
      MaKhoa: "",
    };
  },
  methods: {
    addStudent() {
      const student = {
        maSV: this.maSV,
        tenSV: this.tenSV,
        NgaySinh: this.NgaySinh,
        GioiTinh: this.GioiTinh,
        MaKhoa: this.MaKhoa,
      };
      this.$emit("add", student);
      this.clearForm();
    },
    updateStudent() {
      const updatedStudent = {
        maSV: this.maSV,
        tenSV: this.tenSV,
        NgaySinh: this.NgaySinh,
        GioiTinh: this.GioiTinh,
        MaKhoa: this.MaKhoa,
      };
      this.$emit("update", updatedStudent);
      this.clearForm();
    },
    clearForm() {
      this.maSV = "";
      this.tenSV = "";
      this.NgaySinh= "",
      this.GioiTinh= "",
      this.MaKhoa= ""
    },
  },
  watch: {
    editedStudent(newStudent) {
      if (newStudent) {
        this.maSV = newStudent.maSV;
        this.tenSV = newStudent.tenSV;
        this.NgaySinh = newStudent.NgaySinh;
        this.GioiTinh = newStudent.GioiTinh;
        this.MaKhoa = newStudent.MaKhoa;
      }
    },
  },
};
</script>
<style scoped>
button {
  background-color: blue;
  color: white;
  padding: 5px 10px;
  border: none;
  cursor: pointer;
}

button:hover {
  background-color: darkblue;
}

input[type="text"] {
  padding: 5px;
  margin-bottom: 10px;
  width: 200px;
}
</style>
