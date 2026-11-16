<script setup>
import router from '@/router';
import { reactive, ref } from 'vue';
import axios from 'axios'; // import thư viện axios để call api

// khởi tạp biến để lưu dữ liệu sản phẩm người dùng nhập vào form
const product = reactive({
    name: '',
    price: '0',
    image: '',
})

const handleSubmit = async () => {
    try {
        // call api để gửi lên json-sever
        await axios.post(
            'http://localhost:3000/products', // URL API
            product // dữ liệu người dùng nhập vào form
        );
        router.push('/List'); // chuyển hướng sang trang List.vue
    } catch (error) {
        console.log(error);
        
    }
}

</script>

<template>
    <div>
        <h1>Create Page</h1>
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