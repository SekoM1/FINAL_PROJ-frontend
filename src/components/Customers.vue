<template>
<section class = "testimonial section-py">
     

        <div class="container">
          <div class="row">
             <!-- title -->
      <div class = "title">
        <h2>Why Our Customers Love Us</h2>
      </div>
      <!-- end of title -->
          </div>
          <div id="carouselExampleCaptions" class="carousel slide" data-bs-ride="carousel" style="height:400px; text-align:justify;">
            <div class="carousel-indicators">
              <button type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide-to="0" class="active"
                aria-current="true" aria-label="Slide 1"></button>
              <button type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide-to="1"
                aria-label="Slide 2"></button>
              <button type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide-to="2"
                aria-label="Slide 3"></button>
              <button type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide-to="3"
                aria-label="Slide 4"></button>
            </div>

            <div  class="carousel-inner" v-if="Testimonies">
              <div class="carousel-item" :class="{active : isActive === index }" v-for="(testimonial, index) in Testimonies" :key="index">
                <img :src="testimonial.image" class="d-block"
                  style="border-radius: 50%; width: 150px; height: 150px; margin: 60px auto 30px; object-fit: cover;"
                  alt="A picture of my work">
                <div class="testimonial-content" style="color: black;">
                  <h5>{{testimonial.name}}</h5>
                  <p style="font-style: italic;">{{testimonial.testimony}}</p>
                </div>
              </div>
            </div>
          </div>
        </div>
</section>
</template>

<script>

  export default {
  data() {
    return {
      Testimonies: null,
      isActive: 0,
    };
  },
  mounted() {
    fetch("")
      .then((res) => res.json())
      .then((data) => {
        console.log(data);
        this.Testimonies = data;
      });
  },

}
</script>

<style>
.testimonial{
    background: linear-gradient(rgba(0, 0, 0, 0.7), rgba(0, 0, 0, 0.7)), url(../assets/header-banner.jpg) center/cover no-repeat fixed;
    overflow: hidden;
}
.testimonial .title{
    text-align: center;
    color: #fff;
}
.testimonial-slider{
    margin: 2rem 0;
}
.testimonial-item img{
    width: 180px;
    height: 180px;
    border-radius: 50%;
    margin: 0 auto;
}
.testimonial-item{
    text-align: center;
}
.testimonial-item p{
    color: #fff;
    font-size: 1.2rem;
    line-height: 1.7;
    width: 80%;
    margin: 1.5rem auto 1rem;
    color: var(--lightGrey);
    opacity: 0.9;
}
.testimonial-item h3{
    color: var(--grey);
}

</style>