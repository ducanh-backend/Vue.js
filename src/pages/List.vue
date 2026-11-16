<script setup>
// call api
import router from '@/router';
import axios from 'axios';
import {onMounted, ref} from 'vue'; // Tự động thực thi hàm khi component được 

const products = ref([]); // khởi tạo biến
const getListProducts = async () => {   // khai báo hàm lấy danh sách sản phẩm từ json - server
    const response = await axios.get('http://localhost:3000/products');
    // gán dư liệu trả về cho biến products
    products.value = response.data;
    console.log(products.value); 
}

const deleteProduct = async (id) => {
    if (confirm('Bạn có chắc muốn xóa sản phẩm này?')) { // khai báo hàm xóa sản phẩm theo id
        await axios.delete(`http://localhost:3000/products/${id}`);
        getListProducts(); // gọi lại hàm getListProducts để load lại danh sách sản phẩm
    }
}
const editProduct = (id) => {
    router.push(`/Edit/${id}`); // chuyển hướng sang trang Edit.vue theo id
}
onMounted(() => {
    getListProducts(); // tự động thực thi hàm khi load List.vue
})
</script>



<template>
    <router-link to="/Create">Create Product</router-link>
    <table>
        <thead>
            <tr>
                <th>ID</th>
                <th>Name</th>
                <th>Price</th>
                <th>Image</th>
                <th>Actions</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="p in products" :key="p.id">
                <td>{{p.id}}</td>
                <td>{{p.name}}</td>
                <td>{{p.price}}</td>
                <td><img :src="p.image" alt="" width="100px"></td>
                <td>
                    <button @click="deleteProduct(p.id)">Delete</button>
                    <button @click="editProduct(p.id)">Edit</button>
                </td>
            </tr>
        </tbody>
    </table>
    <div>
        <h1>List Page</h1>
    </div>
</template>