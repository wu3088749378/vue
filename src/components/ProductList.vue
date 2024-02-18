<template>
  <div>
    <h2>ProductList</h2>
    <ul>
      <li v-for="product in products" :key="product.id">
        <h3>{{ product.name }}</h3>
        <p>Price: ${{ product.price }}</p>
        <p v-if="product.reviews.length > 0">
          Average Rating: {{ calculateAverageRating(product.reviews) }}
        </p>
        <p v-else></p>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      products: []
    };
  },
  created() {
    this.products = [
      {
        id: 1,
        name: "Product1",
        description: "Description for Product1",
        price: 99.99,
        category: {
          id: 1,
          name: "Electronics"
        },
        images: ["image1.jpg", "image2.jpg"],
        reviews: [
          {
            id: 1,
            rating: 4,
            comment: "Great product!",
            author: "John Doe"
          },
          // 更多评论...
        ]
      },
      // 更多商品...
    ];
  },
  methods: {
    calculateAverageRating(reviews) {
      if (reviews.length === 0) return 0;
      
      // 计算评分的总和
      const totalRating = reviews.reduce((sum, review) => sum + review.rating, 0);
      
      // 计算平均评分
      return (totalRating / reviews.length).toFixed(1);
    }
  }
};
</script>

<style>
</style>
