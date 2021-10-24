<template>
  <div class="product">
    <b-row class="flex-row justify-content-between">
      <b-card style="max-width: 25rem;" class="mt-4 mx-4 border rounded shadow">
          <b-row>
              <b-col class="rounded">
                  <b-img class="rounded" width="200" height="200" :src="products.images[selectedcolor]" :key="selectedcolor"></b-img>
                  <b-row >
                      <b-col class="mt-2 d-flex align-items-center">
                          <b-form-rating class="mx-1" :class="selectedcolor" :value="products.stars" show-clear no-border readonly></b-form-rating>
                      </b-col>
                  </b-row>
                  <b-row>
                    <b-col class="color-select d-flex align-items-center justify-content-center">
                      <div v-for="(item,index) in products.availableColor" :key="index">
                        <b-icon class="mx-1" :class="item" @click="changeColor(item)" icon="circle-fill" aria-hidden="true"></b-icon>
                      </div> 
                    </b-col>
                  </b-row>
                  <b-row>
                    <div class="sizes">
                      <span :class="selectedcolor">Size:</span>
                      <div class="size-box" :class="selectedcolor" v-for="(item, index) in products.sizes" :key="index">
                        <input class="rounded" :class="selectedcolor"
                          type="button"
                          :value="item"
                          @click="changeSizes(item)"
                        />
                      </div>
                    </div>
                  </b-row>                                    
              </b-col>
              <b-col class="mt-1">
                  <b-row class=mt-1>
                    <b-card-text class="text-left product-headername" :class="selectedcolor">
                        {{products.name}}
                    </b-card-text>
                  </b-row>
                  <b-row class=mt-1>
                    <b-card-text class="text-left product-lname" :class="selectedcolor">
                        {{products.lname}}
                    </b-card-text>
                  </b-row>
                  <b-row class=mt-1>
                    <b-card-text class="text-left product-price" :class="selectedcolor">
                        $ {{comPutedPrice =changePrice}}
                    </b-card-text>
                  </b-row>
                  <b-row class="mt-1">
                    <b-card-text class="w-100 text-left product-desc" :class="selectedcolor">
                        {{products.description}}
                    </b-card-text>
                  </b-row>
                  <b-row class="mt-1 justify-content-center align-content-center">                
                    <b-col class ="d-flex justify-content-center align-content-center">
                        <b-icon class="mx-1" :class="selectedcolor" @click="decrement" icon="dash-circle" aria-hidden="true"></b-icon>
                        <span class= "mx-1" :class="selectedcolor" >{{quantity}}</span>
                        <b-icon class="mx-1" :class="selectedcolor" @click="incerment" icon="plus-circle" aria-hidden="true"></b-icon>
                    </b-col> 
                  </b-row>
                  <b-row>
                    <b-col class="mt-3 d-flex align-items-center justify-content-center">
                      <b-button @click="addToBasket()" variant="gray" :class="selectedcolor" href="#" >Add Cart</b-button>
                    </b-col>                
                  </b-row>                   
              </b-col>                 
          </b-row>
      </b-card> 
    </b-row>
   
  </div>
</template>

<script>
export default {
  name: 'ProductCard',
  props:{products:Object},
  
  data(){
    return {
      quantity:1,
      selectedcolor:this.products.availableColor[0],
      sizes:this.products.sizes[0],
      comPutedPrice:this.products.price
    }

  },
  computed:{
    changePrice(){
      return this.products.price + this.products.price * (this.sizes / 10)
    }
  },
  methods:{
      decrement(){
          if(this.quantity != 1){
            this.quantity--;
          }
      },
      incerment(){
          this.quantity++;
      },
      changeColor(val){
        this.selectedcolor = val;
      },
      changeSizes(val){
        this.sizes=val;
      },
      addToBasket(){
        //Ref Ata
        let obj = {
          id:this.products.id,
          name:this.products.lname,
          color:this.selectedcolor,
          size: this.sizes,
          quantity:this.quantity,
          price:this.comPutedPrice,
          image:this.products.images[this.selectedcolor],
        }
        this.$emit('addProduct',obj)
      }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.pink{
  color: #CCA9A8;
  border-color: #CCA9A8;
}

.mint{
  color: #98C8CA;
  border-color: #98C8CA;
}
.blue{
  color: #4EA8CA;
  border-color: #4EA8CA;
}


.text-left{
  text-align: left;
}
.product-headername {
  text-transform: uppercase;
  font-size: 10px;
  margin-bottom:0.1vh;
  font-family: 'Roboto', sans-serif;
}

.product-lname {
  text-transform: uppercase;
  margin:0.1vh;
  font-size:15px;
  font-family: 'Roboto', sans-serif;
}
.product-price {
  text-transform: uppercase;
  font-family: 'Roboto', sans-serif;
}
.product-desc {
  text-transform: uppercase;
  font-size:10px;
  margin:0.1vh;
  font-family: 'Roboto', sans-serif;
}
.sizes {
  width: 100%;
  display: flex;
  height: 55px;
  align-items: center;
}
.size-box {
  display: flex;
  justify-content: flex-end;
  width: 100%;
  position: relative;
  appearance: none;
  margin: 1px;
  
}
.size-box label {
  position: absolute;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 40px;
  color: white;
  font-weight: 600;
  font-size: 16px;
  font-family: "Tahoma", Arial, sans-serif;
}
.sizes span {
  margin-right: 10px;
}
input[type="radio"] {
  width: 40px;
  height: 40px;
  position: relative;
  padding: 0.5rem;
  color:#42b983;
  border-radius: 0.5rem;
}
input[type="radio"]:checked {
  border: 3px solid red;
}


</style>
