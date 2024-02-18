<template>
  <div>
    <ZuJian>
      <div>
        <h1>Hello, World!</h1>
        <p>This is my content.</p>
      </div>
    </ZuJian>
  <ProductList>
  </ProductList>
  <HouTai>
  </HouTai>
  <CardComponent>
  </CardComponent>
  <UserManagementComponent>
  </UserManagementComponent>
  </div>
</template>

 


<script>
// 导入自定义组件 MyContainer
import ZuJian from '@/components/ZuJian.vue';
import ProductList from '@/components/ProductList.vue';
import HouTai from '@/components/HouTai.vue';
import CardComponent from '@/components/CardComponent.vue';
import UserManagementComponent from '@/components/UserManagementComponent.vue';


export default {
  components: {
    ZuJian,// 注册 ZuJian 组件
    ProductList, // 注册 ProductList 组件
    HouTai, // 注册 HouTai 组件
    CardComponent, // 注册 CardComponent 组件
    UserManagementComponent // 注册 UserManagementComponent 组件
  }
};
</script>
