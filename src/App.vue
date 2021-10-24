<template>
  <div id="app">
    <b-navbar class="nav-bar-class px-5" toggleable="sm" type="dark">
        <b-navbar-brand href="#">Shoe's Shop</b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav class="mx-3">
            <b-nav-item href="#">Homepage</b-nav-item>
            <b-nav-item href="#">Men</b-nav-item>
            <b-nav-item href="#">Women</b-nav-item>
          </b-navbar-nav> 
        </b-collapse>
          <b-dropdown class="item d-flex justify-content-end" variant="gray" no-caret>
            <template #button-content>
                <b-icon class="cart-icon" icon="cart4"></b-icon>
                <b-badge class="mx-2" size="sm">{{addBasket.length}}</b-badge>
            </template>           
            <b-dropdown-form v-for="(el,i) in addBasket" :key="i">
              <div class="cart">
                <div class="d-flex align-items-center">
                    <b-col>
                      <img height="100" width="100" :src="el.image" class="cart-img rounded-3"/>
                    </b-col>
                    <b-col>
                          <p class="item-name m-1">{{el.name}}</p>
                          <p class="item-size mx-1 ">Size : {{el.size}}</p>
                          <p class="item-price m-1 mb-1">Price $ {{el.price * el.quantity}}</p>
                          <b-col class="d-flex align-items-center justify-content-between">
                              <b-icon variant="danger" @click="el.quantity--,el.quantity<1 ? el.quantity=1:''" icon="dash-circle" aria-hidden="true"></b-icon>
                              <p class="m-0">{{el.quantity}}</p>
                              <b-icon variant="success" @click="el.quantity++" icon="plus-circle" aria-hidden="true"></b-icon>
                              <button type="button" @click="deleteProduct(el)" class="btn btn-secondary mx-1"><b-icon icon="trash-fill"></b-icon>
                              </button>
                          </b-col>                      
                    </b-col>
                </div>
              </div>
            </b-dropdown-form>
          </b-dropdown>
      </b-navbar>
      <div class="d-flex justify-content-center flex-wrap w-100 align-items-center">
        <ProductCard v-for="(item,index) in products" :key="index" :products="item" @addProduct="addProduct" />
      </div>
  </div>
</template>

<script>
import ProductCard from './components/ProductCard.vue'


export default {
  name: 'App',
  components: {
    ProductCard,
  },
  data(){
    return {
        products:[
          {
            id:1,
            name: "Women Running Shoes",
            lname:"Nike Epic React Flyknit Pearl Pink",
            price:100,
            description:"Nike React Infinity Run Flyknit 2 ile koşmayı asla bırakma.",
            stars:3.5,
            quantity:1,
            availableColor:["pink","mint","blue"],
            images:
              {
                pink:require(`@/assets/images/pink.png`),
                mint:require(`@/assets/images/mint.png`),
                blue:require(`@/assets/images/blue.png`),
              },
            sizes:[5,6,7,8,9,10],  
          },
          {
            id:2,
            name: "Men Running Shoes",
            lname:"Nike Epic React Flyknit Ocean Blue",
            price:100,
            description:"Nike React Infinity Run Flyknit 2 ile koşmayı asla bırakma.",
            stars:4.5,
            quantity:1,
            availableColor:["pink","mint","blue"],
            images:
              {
                pink:require(`@/assets/images/pink.png`),
                mint:require(`@/assets/images/mint.png`),
                blue:require(`@/assets/images/blue.png`),
              },
            sizes:[5,6,7,8,9,10],  
          },
          {
            id:3,
            name: "Child Running Shoes",
            lname:"Nike Epic React Flyknit Night Dark",
            price:100,
            description:"Nike React Infinity Run Flyknit 2 ile koşmayı asla bırakma.",
            stars:2.5,
            quantity:1,
            availableColor:["pink","mint","blue"],
            images:
              {
                pink:require(`@/assets/images/pink.png`),
                mint:require(`@/assets/images/mint.png`),
                blue:require(`@/assets/images/blue.png`),
              },
            sizes:[5,6,7,8,9,10],                      
          },
          {
            id:4,
            name: "Child Sports Shoes",
            lname:"Nike Epic React Flyknit Smoke Blue",
            price:100,
            description:"Nike React Infinity Run Flyknit 2 ile koşmayı asla bırakma.",
            stars:3.1,
            quantity:1,
            availableColor:["pink","mint","blue"],
            images:
              {
                pink:require(`@/assets/images/pink.png`),
                mint:require(`@/assets/images/mint.png`),
                blue:require(`@/assets/images/blue.png`),
              },
            sizes:[5,6,7,8,9,10],  
          },
        ],
        addBasket:[],
    }
  },
  methods:{
    addProduct(e){
      let isFound=null
      isFound = this.addBasket.find(item=> item.id==e.id && item.color==e.color && item.size==e.size)
      if(!isFound){
        console.log("emited")
        this.addBasket.unshift(e)
      }else{
        isFound.quantity+=e.quantity
      }
    },
    deleteProduct(value){
      this.addBasket.splice(value,1);
    },
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.nav-bar-class{
  background-color: rgb(170, 98, 170);
}
.item {
  position:absolute;
  right: 0px;
}

.cart-icon {
  color: whitesmoke;
}



</style>
