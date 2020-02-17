<template>
    <div class="micro">
        <div class="data-from-lumen">
            <h2>Fetched Data From Lumen Service</h2>
            <ul class="users">
                <li v-for="user in users" v-bind:key="user.email">Name: {{user.name}}, Email: {{user.email}}</li>
            </ul>
        </div>
        <div class="data-from-nestjs">
            <h2>Fetched Data From NestJs Service</h2>
            <ol class="products">
                <li v-for="product in products" v-bind:key="product.id">Product Id: {{product.id}}, Product Name: {{product.name}}</li>
            </ol>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                name: 'Hasan',
                users: [],
                products: []
            }
        },
        created() {
            this.getProduct();
            this.getUser();
        },
        methods: {
            async getProduct () {
                const res = await this.axios.get('http://localhost:3000/products');
                this.products.push(...res.data);
            },
            async getUser() {
                const res = await this.axios.get('http://localhost:9000/user');
                this.users.push(...res.data);
            }
        }
    }
</script>
<style scoped>
    .micro {
        width: 1170px;
        margin: auto;
    }
    .data-from-lumen,
    .data-from-nestjs {
        border: 1px solid #afafaf;
        width: 45%;
        margin-left: 10px;
        display: inline-block;
    }
    .products, .users {
        text-align: left;
    }
</style>
