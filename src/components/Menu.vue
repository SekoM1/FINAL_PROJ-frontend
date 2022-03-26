<template>
  <section id = "menu" class = "menu section-py">
      <!-- title -->
      <div class = "title">
        <h4>Taste Our Food</h4>
        <h2>Quality food items</h2>
      </div>

      <!-- Button trigger modal -->
<button type="button" class="btn btn-outline" data-bs-toggle="modal" data-bs-target="#addmenu">
  ADD MENU ITEM
</button>

<!-- Modal -->
<div class="modal fade" id="addmenu" tabindex="-1" aria-labelledby="addmenuLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="addmenuLabel">Modal title</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
        <form @submit.prevent="createMenu">
        <ul>
         <li>Tittle </li>
          <li> <input v-model="title" required type="text"></li>
          <li>Price</li>
          <li> <input v-model="price" required type="number"></li>
        <li>desc</li>
        <li> <input v-model="desc" required type="text"></li>
        <li>categories</li>
        <li> <input v-model="categories" required type="text"></li>
        <li>img</li>
        <li> <input v-model="img" required type="text"></li>
       </ul>
       
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cancel</button>
        <button type="submit" class="btn btn-primary">Save</button>
       </form>
      </div>
     
    </div>
  </div>
</div>

      <!-- end of title -->
  <!-- <div class="container"> -->
        <!-- first row -->
    <div class="row" style="row-gap:20px;">
    <div class="col-lg-4 col-md-6 col-sm-12" v-for="menu in menus" :key="menu._id">
      <!-- item -->
         
              <div class = "menu-item" v-if="menu">
          <!-- <a href = "@/assets/food-american-breakfast.jpg"> -->
            <img :src ="menu.img" alt = "food image" style="height: 310px; object-fit: cover;">
            <div class = "menu-overlay">
              <div class = "menu-overlay-content">
                <div>
                  <h2>{{menu.title}}</h2>
                  <h2>R{{menu.price}}</h2>
                </div>
                <h5>{{menu.desc}}</h5>
              </div>
            </div>
          <!-- </a> -->
        </div>
    </div>
        <!-- end of item -->
    
    <!-- <div class="col-lg-4 col-md-6 col-sm-12"> -->
      <!-- item -->
        <!-- <div class = "menu-item">
          <a href = "@/assets/food-chicken-soup.jpg">
            <img src = "@/assets/food-chicken-soup.jpg" alt = "food image">
            <div class = "menu-overlay">
              <div class = "menu-overlay-content">
                <div>
                  <h2>chicken soup</h2>
                  <h2>R25</h2>
                </div>
                <h5>delicious / healthy / cheap</h5>
              </div>
            </div>
          </a>
        </div> -->
    <!-- </div> -->
        <!-- end of item -->
    
    <!-- <div class="col-lg-4 col-md-6 col-sm-12"> -->
      <!-- item -->
        <!-- <div class = "menu-item">
          <a href = "@/assets/food-chinese-noodles.jpg">
            <img src = "@/assets/food-chinese-noodles.jpg" alt = "food image">
            <div class = "menu-overlay">
              <div class = "menu-overlay-content">
                <div>
                  <h2>chinese noodles</h2>
                  <h2>R25</h2>
                </div>
                <h5>delicious / healthy / cheap</h5>
              </div>
            </div>
          </a>
        </div>
          </div> -->
        <!-- end of item -->
    </div>
  
    <!-- second row -->
   <!-- <div class="row"> -->
    <!-- <div class="col-lg-4 col-md-6 col-sm-12"> -->
      <!-- item -->
        
           <!-- <div class = "menu-item">
          <a href = "@/assets/food-cake.jpg">
            <img src = "@/assets/food-cake.jpg" alt = "food image">
            <div class = "menu-overlay">
              <div class = "menu-overlay-content">
                <div>
                  <h2>cake items</h2>
                  <h2>R25</h2>
                </div>
                <h5>delicious / healthy / cheap</h5>
              </div>
            </div>
          </a>
        </div> -->
        <!-- end of item -->
    <!-- </div> -->
    <!-- <div class="col-lg-4 col-md-6 col-sm-12"> -->
      <!-- item -->
        
           <!-- <div class = "menu-item">
          <a href = "@/assets/food-cake.jpg">
            <img src = "@/assets/food-cake.jpg" alt = "food image">
            <div class = "menu-overlay">
              <div class = "menu-overlay-content">
                <div>
                  <h2>cake items</h2>
                  <h2>R25</h2>
                </div>
                <h5>delicious / healthy / cheap</h5>
              </div>
            </div>
          </a>
        </div> -->
        <!-- end of item -->
    <!-- </div> -->
    <!-- <div class="col-lg-4 col-md-6 col-sm-12"> -->
       <!-- item -->
        <!-- <div class = "menu-item">
          <a href = "@/assets/food-indian-food.jpg">
            <img src = "@/assets/food-indian-food.jpg" alt = "food image">
            <div class = "menu-overlay">
              <div class = "menu-overlay-content">
                <div>
                  <h2>indian dish</h2>
                   <div class="btn" @click="goToBlog1()">
                  <a href="#blog1" class="btn"><b>more ...</b></a>
                </div>
                </div>
                <h5>delicious / healthy / cheap</h5>
              </div>
            </div>
          </a>
        </div> -->
        <!-- end of item -->
    <!-- </div> -->
  <!-- </div> -->
  <!-- </div> -->
  


</section>
</template>

<script>
export default {
  data() {
    return {
       title: "",
    desc: "",
    img: "",
   category: "",
    price: "",
    menus:null
    };
  },
  mounted() {
    if (!localStorage.getItem("jwt")) {
        alert("User not logged in");
       
      }
    fetch("https://lyf-styl-reservation.herokuapp.com/menu", {
      method: "GET",
      headers: {
        "Content-type": "application/json; charset=UTF-8",
       "Authorization": `Bearer ${localStorage.getItem("jwt")}`}
    })
      .then((response) => response.json())
      .then((json) => {
        console.log(json)
        this.menus = json;
      });
  },
  methods: {
createMenu() {
        
      if (!localStorage.getItem("jwt")) {
        alert("User not logged in");
       
      }
    fetch("https://lyf-styl-reservation.herokuapp.com/menu/add", {
        method: "POST",
        body: JSON.stringify({
          title: this.title,
         category: this.category,
          desc: this.desc,
          img:this.img,
          price: this.price,

    
        }),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
          Authorization: `Bearer ${localStorage.getItem("jwt")}`,
        },
      })
        .then((response) => response.json())
    
        .then((json) => {
         console.log(json)
          alert("item added");
         
        })
        .catch((err) => {
          console.log(err)
          alert("It failed.Try again please");
          this.loading = false;
        });
    },
}
}
</script>

<style scoped>
.menu.section-py{
    padding-bottom: 0;
   
}
.menu .title{
    text-align: center;
}
section#menu{
  display: flex;
  flex-direction: column;
}
/* .menu-wrap{
  display: flex;
  flex-direction: column;
} */
.first-menu {
  display: flex;
  gap: 10px;
  margin: 5px;
}

.second-menu {
  display: flex;
  margin: 5px;
  gap: 10px;
}
.title{
    padding: 0.2rem;
}
.menu-wrapper{
    margin-top: 2rem;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
}
.menu-item{
    position: relative;
    cursor: pointer;
}
.menu-overlay{
    height: 130px;
    background: rgba(0, 0, 0, 0.8);
    position: absolute;
    bottom: 0;
    width: 100%;
    color: #fff;
    padding: 1.5rem;
    opacity: 0;
    transition: var(--transition);
    overflow: hidden;
}
.menu-overlay-content{
    overflow: hidden;
    transition: all 0.5s ease;
    transform: translateY(100%);
    margin-top: -35px;
    text-size-adjust: 40px;
}
.menu-overlay-content div{
    display: flex;
    justify-content: space-between;
}
.menu-overlay-content h2{
    text-transform: capitalize;
    margin-bottom: 0;
}
.menu-overlay-content h5{
    text-transform: uppercase;
    color: var(--grey);
    margin-top: 0.6rem;
    font-size: 0.8rem;
}
.menu-item:hover .menu-overlay{
    opacity: 1;
}
.menu-item:hover .menu-overlay-content{
    transform: translateY(0);
}
/* @media screen and (min-width: 678px){
    .menu-wrapper{
        display: grid;
        grid-template-columns: repeat(2, 1fr);
    }
} */
</style>