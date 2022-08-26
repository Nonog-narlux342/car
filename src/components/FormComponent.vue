<template>
  <form @submit.prevent="submitForm">
    <div>
      <label for="emp-name">ทะเบียนรถ</label>
      <input type="text" class="form-control" v-model.trim="employee.name" />
    </div>
    <div>
      <label for="type">ประเภทของรถ</label>
      <select class="form-select" v-model="employee.type">
        <option value="รถบรรทุก">รถบรรทุก</option>
        <option value="รถกระบะ">รถกระบะ</option>
        <option value="รถเก๋ง">รถเก๋ง</option>
      </select>
    </div>
    <div>
      <label for="formFile" class="form-label">รูปรถ</label>
      <input class="form-control" type="file" id="formFile" />
    </div>
    <div>
      <label for="daynew">วันที่จดทะเบียน</label>
      <input
        type="text"
        class="form-control"
        placeholder="วว/ดด/ปป"
        v-model.trim="employee.daynew"
      />
    </div>
    <div>
      <label for="dayold">วันที่ทะเนียนหมดอายุ</label>
      <input
        type="text"
        class="form-control"
        placeholder="วว/ดด/ปป"
        v-model.trim="employee.dayold"
      />
    </div>
    <div>
      <button>บันทึกข้อมูล</button>
    </div>
  </form>
  <hr />
  <form>
    <div class="card">
  <div class="card-body">
    <h5 class="card-title">เลขทะเบียน: {{employee.name}}</h5>
    <p class="card-text">เป็นรถ: {{employee.type}} วันที่จดทะเบียน | วันที่ทะเนียนหมดอายุ</p>
    <p class="card-text">วันที่จดทะเบียน: {{employee.daynew}} | วันที่ทะเนียนหมดอายุ: {{employee.dayold}}</p>
  </div>
</div>
    <ul>
      <div
        v-for="(item, index) in employee"
        :key="index"
        :name="item.name"
      ></div>
    </ul>
  </form>
</template>

<script>
export default {
  name: "FormComponent",
  data() {
    return {
      employee: {
        name: "",
        type: "",
        daynew: "",
        dayold: "",
      },
    };
  },
  methods: {
    submitForm() {
      const newEmployee = {
        name: this.employee.name,
        type: this.employee.type,
        daynew: this.employee.daynew,
        dayold: this.employee.dayold,
      };
      this.$emit("save", newEmployee);
      this.resetForm();
    },
    resetForm() {
      this.employee.name = "";
      this.employee.type = "";
      this.employee.daynew = "";
      this.employee.dayold = "";
    },
  },
  props: ["employees"],
};
</script>

<style scoped>
form {
  margin: 2rem auto;
  max-width: 40rem;
  border-radius: 12px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.25);
  padding: 2rem;
  background: #fff;
}
.form-control {
  margin: 0.5rem 0;
}
label {
  font-weight: bold;
}
input,
select {
  display: block;
  width: 100%;
  font: inherit;
  margin-top: 0.5rem;
}
button {
  font: inherit;
  background: rgb(88, 88, 202);
  color: white;
  cursor: pointer;
  padding: 0.5rem 1rem;
  border-radius: 15px;
}
input[type="radio"],
input[type="checkbox"] {
  display: inline-block;
  width: auto;
  margin-right: 1rem;
}
input[type="radio"] + label,
input[type="checkbox"] + label {
  font-weight: normal;
}
h2 {
  font-size: 1rem;
  margin: 0.5rem 0;
}
</style>