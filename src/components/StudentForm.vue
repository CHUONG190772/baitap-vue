<template>
  <div>
    <input type="text" v-model="maSV" placeholder="Mã sinh viên" />
    <br>
    <input type="text" v-model="tenSV" placeholder="Tên sinh viên" />
    <br>
    <input type="Date" v-model="NgaySinh" placeholder="Ngày Sinh" />
    <br><br>
    <!-- <input type="text" v-model="GioiTinh" placeholder="Giới tính" /> -->
    <!-- <select v-model="GioiTinh" placeholder="Giới tính">
      <option value="Nam">Nam</option>
      <option value="Nữ">Nữ</option>
      <option value="Khác">Khác</option>
    </select> -->
    <label>
      <input type="checkbox" v-model="isNam" />
      Nam
    </label>
    <label>
      <input type="checkbox" v-model="isNu" />
      Nữ
    </label>
    <label>
      <input type="checkbox" v-model="isKhac" />
      Khác
    </label>
    <br><br>
    <!-- <input type="text" v-model="MaKhoa" placeholder="Mã Khoa" /> -->
    <select v-model="MaKhoa" placeholder="Mã Khoa">
      <option value="CNTT">CNTT</option>
      <option value="Marketing">Marketing</option>
      <option value="Business">Business</option>
    </select>
    <br><br>
    <button @click="addStudent"><i class="fa-solid fa-user-plus"></i></button>
    <button v-if="editedStudent" @click="updateStudent"> <i class="fa-solid fa-check"></i></button>
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
      isNam: false,
      isNu: false,
      isKhac: false,
      MaKhoa: "",
    };
  },
  methods: {
    addStudent() {
      const student = {
        maSV: this.maSV,
        tenSV: this.tenSV,
        NgaySinh: this.NgaySinh,
        GioiTinh: this.getGioiTinh(),
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
        GioiTinh: this.getGioiTinh(),
        MaKhoa: this.MaKhoa,
      };
      this.$emit("update", updatedStudent);
      this.clearForm();
    },
    clearForm() {
      this.maSV = "";
      this.tenSV = "";
      this.NgaySinh= "",
      this.isNam = false;
      this.isNu = false;
      this.isKhac = false;
      this.MaKhoa= ""
    },
    getGioiTinh() {
      const gioiTinhArr = [];
      if (this.isNam) gioiTinhArr.push('Nam');
      if (this.isNu) gioiTinhArr.push('Nữ');
      if (this.isKhac) gioiTinhArr.push('Khác');
      return gioiTinhArr.join(', ');
    },
  },
  watch: {
    editedStudent(newStudent) {
      if (newStudent) {
        this.maSV = newStudent.maSV;
        this.tenSV = newStudent.tenSV;
        this.NgaySinh = newStudent.NgaySinh;
        const gioiTinhArr = newStudent.GioiTinh.split(', ');
        this.isNam = gioiTinhArr.includes('Nam');
        this.isNu = gioiTinhArr.includes('Nữ');
        this.isKhac = gioiTinhArr.includes('Khác');
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
  border-radius: 10px ;
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
