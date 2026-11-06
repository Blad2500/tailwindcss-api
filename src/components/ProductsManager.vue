<script setup>
import { createProduct } from '../api/products';

 </script>

<script> 
 export default{
    name : "ProductsManager",
    data(){
        return{
            products: [],
            newproduct: {
                name: "",
                price: 0,
                instock: false
            }
        }
    },
    methods:{
        async loadProducts(){
            this.products = await getProducts();
        },
        async addProduct(product) {
            await createProduct(product);
            await this.loadProducts();  
        },
        async submitCreateProduct(){
            await this.addProduct(this.newproduct);
        }
    },
    mounted(){
        this.loadProducts();
    }
}
 
 </script>

 <template>
    <main class="flex flex-col justify-center items-center">
        <h1 class="">Termékek Management</h1>

        <table class="flex flex-col w-full">
            <thead class="p-2 w-full">
                <tr class="flex justify-around gap-12">
                    <th class="">id</th>
                    <th class="">name</th>
                    <th class="">price</th>
                    <th class="">in stock</th>
                </tr>
            </thead>
            <tbody class="p-2 w-full">
                <tr v-for="product in products" class="flex justify-around gap-8" :key="product.id">
                    <td class="">{{ product.id }}</td>
                    <td class="">{{ product.name }}</td>
                    <td class="">{{ product.price }}</td>
                    <td class="">{{ product.instock ? "igen" : "elfogyott" }}</td>
                </tr>
            </tbody>
        </table>

        <form @submit.prevent="submitCreateProduct" class="mt-30 flex flex-col border-2 border-stone-200 rounded-xl p-5">

            <label for="name">Name:</label>
            <input type="text" v-model="newproduct.name" name="name" class="border-2 border-stone-200 rounded-xl p-2">

            <label for="price">Price:</label>
            <input type="number" v-model="newproduct.price" name="price" class="border-2 border-stone-200 rounded-xl p-2">

            <label for="instock">In stock?:</label>
            <input type="checkbox" v-model="newproduct.instock" name="instock" id=""><br>

            <button class="w-full border-2 border-greeen-200 rounded-xl hover:border-green-400" type="submit">Létrehozás</button>

        </form>
    </main>
 </template>