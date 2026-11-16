<script setup>
//khai báo components sẽ sử dụng trong file
import HelloWorld from './components/HelloWorld.vue' 
import TheWelcome from './components/TheWelcome.vue'
//lưu trữ dữ liệu của biến: tự động theo dõi giá trị của biến thay đổi
//và rerender ra giao diện
import { ref } from 'vue'; //thường dùng với kiểu dữ liệu nguyên thủy: string/number/boolean
import { reactive } from 'vue'; //thường dùng cho array/object
//const tenBien = ref(giaTri);
const count = ref(100);  //kiểu dữ liệu number - giá trị là 100.
const name = ref('100'); //kiểu dữ liệu string - giá trị là 100.
const isActive = ref(true); //kiểu dữ liệu boolean - giá trị là true/false
//const tenBien = reactive(giaTri);
const student = reactive({
  //key: value,
  name: 'Ducanh',
  birth: 2004,

})
const students = reactive([
  {
    name: 'Ducanh',
    birth: 2004,
    avatar: "https://picsum.photos/200",
    point: 8,
    status: true,
  },
  {
    name: 'Ducanh',
    birth: 2004,
    avatar: "https://picsum.photos/200/300",
    point: 6,
    status: false,
  },
  {
    name: 'Ducanh',
    birth: 2004,
    avatar: " ",
    point: 10,
    status: true,
  }
])
// data binding: ràng buộc dữ liệu
// 1 chiều: {{ tenBien }} hoặc v-bind
// 2 chiều: v-model: v-model="tenBien"
// event binding: bắt sự kiện  
// dạng đầy đủ:  v-on:event="hamxuly" VD: onclick => v-onn: click= ""
// dạng viết tắt: @event="hamxuly" VD: onclick => @click=""
// 
const username = ref('Ducanh');
const demClick = () => {
  count.value++; // tăng biến count lên 1 đơn vị
}
const luiClick = () => {
  count.value--; // giảm biến count xuống 1 đơn vị
}
const doiTrangThai = (index) => {
  // console.log(index);
  students[index].status = !students[index].status; //đổi trạng thái của phần tử thứ index trong mảng students
}
  
</script>

<template>
  <!-- <div> v-model: ràng buộc dữ liệu 2 chiều
    <p>{{ username }}</p>
    <input type="text" v-model="username">
    <button @click="username = 'Ducanh'">Reset</button>
  </div> -->
  <div>
    <p>{{ count }}</p>
     <!-- <button v-on:click = "demClick">Click</button> dạng đầy đủ -->
    <button @click = "demClick">Tiến</button> <!-- dạng viết tắt -->
    <button @click = "luiClick">Lùi</button>
  </div>
  <header>
    <h1>Thông tin sinh viên</h1>
    <br>
    <p>Họ tên: {{ student.name }}</p>
    <p>Năm sinh: {{ student.birth }}</p>

    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Birth</th>
          <th>Avatar</th>
          <th>Point</th>
          <th>Status</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <!-- cú pháp của v-for: 
         v-for="sốÍt in sốNhiều" : không cần index
         v-for="(sốÍt,index) in sốNhiều" -->
         <!-- v-if: kiem tra dieu kien, neu dieu kien dung thi hien thi
          v-else-if: neu dieu kien 1 sai va dieu kien 2 dung
         v-else: neu dieu kien 1 va dieu kien 2 cung sai thi hien thi
         v-show: neu dieu kien dung thi hien thi ra -->
          <!-- <tr v-for=(s, index) in students> -->
        <tr v-for="(s, index) in students" :key="index">
        <!-- <tr v-for="s in students"> -->
          <td>{{ s.name }}</td>
          <td>{{ s.birth }}</td>
          <td><img v-bind:src="s.avatar" v-bind:alt="s.name" width="100" height="100" /></td>
          <td>
            <p v-if="s.point < 5">Trượt môn</p>
            <p v-else-if="s.point < 7">Trung bình</p>
            <p v-else-if="s.point < 9">Khá</p>
            <p v-else>Giỏi</p>
          </td>
          <td>
            <!-- <p v-if="s.status == true">Hoat Dong</p> -->
            <p v-show="s.status == true">Hoat Dong</p>
            <p v-show="s.status == false">Không hoạt động</p>
          </td>
          <td>
            <!-- <button @click="s.status = !s.status">Đổi trạng thái</button> -->
             <button @click="doiTrangThai(index)">Đổi trạng thái</button>
          </td>
          
        </tr>
      </tbody>
    </table>
    <!-- <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" /> -->
    <!-- hiển thị dữ liệu của biến {{ tenBien }} -->
    <!-- <h1>{{ count }}</h1>
    <h1>{{ name }}</h1>
    <h1>{{ isActive }}</h1> -->
    <!-- <div class="wrapper">
      <HelloWorld msg="WEB2072.01" />
    </div> -->
  </header>

  <main>
    <TheWelcome />
  </main>
</template>

// ...existing code...
<style scoped>
:root{
  --accent: #2563eb;
  --accent-2: #7c3aed;
  --muted: #6b7280;
  --bg: linear-gradient(180deg,#f8fafc 0%, #eef2ff 100%);
  --card: linear-gradient(180deg,#ffffff 0%, #fbfdff 100%);
  --gap: 1rem;
  --radius: 12px;
  --soft-shadow: 0 8px 30px rgba(15,23,42,0.08);
  --glass: rgba(255,255,255,0.6);
}

div {
  font-family: Inter, ui-sans-serif, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
  color: #0f172a;
  background: var(--bg);
  padding: 1.25rem;
  min-height: 100vh;
  -webkit-font-smoothing:antialiased;
  -moz-osx-font-smoothing:grayscale;
}

/* Card */
header {
  max-width: 1100px;
  margin: 1.25rem auto;
  background: var(--card);
  padding: 1.25rem;
  border-radius: var(--radius);
  box-shadow: var(--soft-shadow);
  line-height: 1.5;
  overflow: hidden;
  transition: transform .18s ease, box-shadow .18s ease;
}
header:hover { transform: translateY(-4px); box-shadow: 0 16px 40px rgba(15,23,42,0.09); }

/* Layout */
.header-grid {
  display: grid;
  grid-template-columns: 320px 1fr;
  gap: 1rem;
  align-items: start;
}

/* Info card */
.info-card {
  background: linear-gradient(180deg, rgba(37,99,235,0.04), rgba(124,58,237,0.03));
  border-radius: 10px;
  padding: 1rem;
  min-height: 160px;
  display: flex;
  flex-direction: column;
  gap: 0.6rem;
}
.info-card h2 { margin: 0; color: var(--accent-2); font-size: 1.05rem; }

/* Controls */
.form-row { display:flex; gap:0.5rem; align-items:center; margin-top:0.5rem; }
input[type="text"]{
  padding: 0.5rem 0.75rem;
  border: 1px solid #e6e9ee;
  border-radius: 8px;
  width: 100%;
  outline: none;
  transition: box-shadow .15s, border-color .15s, transform .12s;
  background: rgba(255,255,255,0.9);
}
input[type="text"]:focus{
  border-color: var(--accent);
  box-shadow: 0 6px 18px rgba(37,99,235,0.10);
  transform: translateY(-1px);
}
button{
  background: linear-gradient(90deg,var(--accent), var(--accent-2));
  color: #000000;
  border: none;
  padding: 0.5rem 0.75rem;
  border-radius: 8px;
  cursor: pointer;
  margin-left: 0.5rem;
  box-shadow: 0 6px 18px rgba(37,99,235,0.10);
  transition: transform .12s ease;
}
button:hover{ transform: translateY(-2px); }

/* Table wrapper */
.table-wrap {
  background: linear-gradient(180deg, rgba(255,255,255,0.9), rgba(255,255,255,0.98));
  border-radius: 10px;
  padding: 0.75rem;
  box-shadow: 0 6px 18px rgba(15,23,42,0.04);
}

/* Table */
table{
  width: 100%;
  border-collapse: separate;
  border-spacing: 0;
  margin-top: 0;
}
thead th{
  text-align: left;
  padding: 0.9rem 0.75rem;
  color: #374151;
  font-weight: 700;
  font-size: 0.95rem;
  border-bottom: 1px solid #eef2ff;
}
tbody td{
  padding: 0.8rem 0.75rem;
  vertical-align: middle;
  border-bottom: 1px solid #f3f6ff;
}

/* Keep avatars always visible and responsive.
   Removed any rule that hides the 3rd column on small screens. */
tbody tr {
  transition: background .12s ease, transform .12s ease;
  border-radius: 8px;
}
tbody tr:hover{ background: rgba(37,99,235,0.03); transform: translateY(-2px); }

/* Avatar: ensure visible, responsive and graceful on load/failure */
td img{
  width: 84px;
  height: 84px;
  max-width: 100%;
  object-fit: cover;
  object-position: center;
  border-radius: 10px;
  display: inline-block !important;
  vertical-align: middle;
  box-shadow: 0 6px 18px rgba(2,6,23,0.06);
  transition: transform .15s ease, opacity .12s ease;
  background-color: #f3f4f6; /* neutral bg if image fails */
}
td img:hover { transform: scale(1.03); }
td img[alt=""] { opacity: 0.85; }

/* Provide a visible fallback when images fail to load:
   the img will show its background color; ensure container doesn't collapse. */
td {
  min-width: 100px;
}

/* Point badges */
.point-badge {
  display:inline-block;
  padding:0.25rem 0.5rem;
  border-radius:999px;
  font-weight:600;
  font-size:0.85rem;
  color:#fff;
}
.point--low{ background: #ef4444; } 
.point--mid{ background: #f59e0b; } 
.point--good{ background: #10b981; } 
.point--top{ background: #6366f1; } 

/* Status */
.status {
  display: inline-block;
  padding: 0.25rem 0.55rem;
  border-radius: 999px;
  font-size: 0.8rem;
  font-weight:600;
}
.status--active{ background: #d1fae5; color: #065f46; }
.status--inactive{ background: #fee2e2; color: #7f1d1d; }

.meta { color: var(--muted); font-size:0.9rem; }

/* Responsive: keep avatar but scale down on small screens */
@media (max-width: 900px) {
  .header-grid { grid-template-columns: 1fr; }
  input[type="text"]{ width: 160px; }
  td img{ width:64px; height:64px; }
}

/* optional subtle caption beneath avatar */
.avatar-caption { font-size: 0.8rem; color: var(--muted); margin-top: 0.25rem; }
</style>
// ...existing code...