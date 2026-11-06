<script setup> </script>

<script> 
 export default{
    name : "ProductsManager",
    data(){
        return{
            products : []
        }
    },
    methods:{
        async loadProducts(){
            this.products = await getProducts();
        }
    }
 }
 </script>

 <template>
    <main class="flex justify-center items-center">
        <h1 class="">Termékek Management</h1>

        <table>
            <tr>
                <th class="">id</th>
                <th class="">name</th>
                <th class="">price</th>
                <th class="">in stock</th>
            </tr>
        </table>
    </main>
 </template>