<template>
    <div class="product">
        <SingleCard
    v-for="prod in product"
    :key="prod.id"
    :product="prod"
    @toggle-details="toggleProductDetails"
  >
    <template v-if="product.showDetails">
      <!-- render product details here -->
    </template>
  
</SingleCard>
    </div>
</template>
  <script>
  import CardComp from "../components/CardComp.vue";

  import SingleCard from "@/components/SingleCard.vue";
  import axios from "axios";
  
  
  export default {
    name: "ProductView",
    components: {
      CardComp,
      SingleCard
    },
    data() {
      return {
        product: [],
        categories: [],
        priceFilters: [
          { label: "Under R50", min: 0, max: 50 },
          { label: "R50 - R100", min: 50, max: 100 },
          { label: "R100 - R200", min: 100, max: 200 },
          { label: "Over R200", min: 200, max: Infinity },
        ],
        selectedCategory: null,
        selectedPriceRange: null,
        searchQuery: "",
        sortOrder: "asc",
      };
    },
    computed: {
      

    },
    methods: {
      async fetchProduct() {
        try {
            const productId = this.$route.params.id;
            const response = await axios.get(`https://micasa.onrender.com/products/${productId}`);
            console.log(`https://micasa.onrender.com/products/${productId}`);
            this.product = response.data.result;
            console.log('Categories:', this.categories);// Debugging
        } catch (error) {
          console.error(error);
        }
      }

    },
    mounted() {
      this.fetchProduct();
    },
  };
  </script>

 
  