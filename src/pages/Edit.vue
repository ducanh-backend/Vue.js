<script setup>
import router from '@/router';
import { onMounted, reactive, ref } from 'vue';
import axios from 'axios'; // import thư viện axios để call api
import { useRoute } from 'vue-router';

// khởi tạp biến để lưu dữ liệu sản phẩm người dùng nhập vào form
const product = ref({
    name: '',
    price: '0',
    image: '',
});

// Lấy id từ URL xuống để lấy thông tin chi tiết + update
const route = useRoute();
const id = route.params.id; // lấy id từ URL xuống

// tạo hàm để lấy thông tin cũ chi tiết 
const getDeltail = async (id) => {
    const response = await axios.get(`http://localhost:3000/products/${id}`);
    product.value = response.data; // gán dữ liệu trả về cho biến product
    
}
onMounted(() => {
    getDeltail(id);
})

const handleSubmit = async () => {
    try {
        // call api để gửi lên json-sever
        await axios.put(
            `http://localhost:3000/products/${id}`, // URL API
            product.value // dữ liệu người dùng nhập vào form
        );
        router.push('/List'); // chuyển hướng sang trang List.vue
    } catch (error) {
        console.log(error);
        
    }
}

</script>

<template>
    <div>
        <h1>Edit Page</h1>
        <form @submit.prevent="handleSubmit()">
            <div>
                <label for="">Name</label>
                <input type="text" v-model="product.name">
            </div>
            <div>
                <label for="">Price</label>
                <input type="text" v-model="product.price">
            </div>
            <div>
                <label for="">Image</label>
                <input type="text" v-model="product.image">
            </div>
            <button type="submit">Create</button>
        </form>
    </div>
</template>