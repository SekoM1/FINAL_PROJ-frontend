<template>
  <section id = "menu" class = "menu section-py">
      <!-- title -->
      <div class = "title">
        <h4>Taste Our Food</h4>
        <h2>Quality food items</h2>
      </div>
      <!-- end of title -->
  <!-- <div class="container"> -->
        <!-- first row -->
    <div class="row">
    <div class="col-lg-4 col-md-6 col-sm-12">
      <!-- item -->
         
              <div class = "menu-item">
          <a href = "@/assets/food-american-breakfast.jpg">
            <img src = "@/assets/food-american-breakfast.jpg" alt = "food image">
            <div class = "menu-overlay">
              <div class = "menu-overlay-content">
                <div>
                  <h2>american breakfast</h2>
                  <h2>R25</h2>
                </div>
                <h5>delicious / healthy / cheap</h5>
              </div>
            </div>
          </a>
        </div>
    </div>
        <!-- end of item -->
    
    <div class="col-lg-4 col-md-6 col-sm-12">
      <!-- item -->
        <div class = "menu-item">
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
        </div>
    </div>
        <!-- end of item -->
    
    <div class="col-lg-4 col-md-6 col-sm-12">
      <!-- item -->
        <div class = "menu-item">
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
          </div>
        <!-- end of item -->
    </div>
  
    <!-- second row -->
   <div class="row">
    <div class="col-lg-4 col-md-6 col-sm-12">
      <!-- item -->
        
           <div class = "menu-item">
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
        </div>
        <!-- end of item -->
    </div>
    <div class="col-lg-4 col-md-6 col-sm-12">
      <!-- item -->
        
           <div class = "menu-item">
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
        </div>
        <!-- end of item -->
    </div>
    <div class="col-lg-4 col-md-6 col-sm-12">
       <!-- item -->
        <div class = "menu-item">
          <a href = "@/assets/food-indian-food.jpg">
            <img src = "@/assets/food-indian-food.jpg" alt = "food image">
            <div class = "menu-overlay">
              <div class = "menu-overlay-content">
                <div>
                  <h2>indian dish</h2>
                  <h2>R25</h2>
                </div>
                <h5>delicious / healthy / cheap</h5>
              </div>
            </div>
          </a>
        </div>
        <!-- end of item -->
    </div>
  </div>
  <!-- </div> -->
  


</section>
</template>

<script>
export default {
computed: {
    filteredServices: function () {
      return this.services.filter((service) => {
        return service.laundry_service.match(this.search);
      });
    },
  },
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