<template>
  <section id = "banner">
            <h2>BOOK YOUR TABLE NOW</h2>
            <div class = "card-container">
                <div class = "card-content">
                    <h3>Reservation</h3>
                    <form  @submit.prevent="submitForm()" >
                        <div class = "form-row">
                            <select id = "days" v-model="days">
                                <option value = "day-select">Select Day</option>
                                <option value = "sunday">Sunday</option>
                                <option value = "monday">Monday</option>
                                <option value = "tuesday">Tuesday</option>
                                <option value = "wednesday">Wednesday</option>
                                <option value = "thursday">Thursday</option>
                                <option value = "friday">Friday</option>
                                <option value = "saturday">Saturday</option>
                            </select>

                            <select id = "hours" v-model="hours">
                                <option value = "hour-select">Select Hour</option>
                                <option value = "10">10: 00</option>
                                <option value = "10">12: 00</option>
                                <option value = "10">14: 00</option>
                                <option value = "10">16: 00</option>
                                <option value = "10">18: 00</option>
                                <option value = "10">20: 00</option>
                                <option value = "10">22: 00</option>
                            </select>
                        </div>

                        <div class = "form-row">
                            <input type = "text" id="fullname" v-model="fullname" placeholder="Full Name">
                            <input type = "text" id="number" v-model="number" placeholder="Phone Number">
                        </div>

                        <div class = "form-row">
                            <input type = "number" id="people" v-model="people" placeholder="How Many Persons?" min = "1">
                            <input type = "submit" value = "BOOK TABLE">
                        </div>
                    </form>
                </div>
            </div>  
        </section>
</template>

<script>
export default {
  data() {
    return {
      form: false,
      people:null,
      hours: null,
      days: null,
      number: null,
    }
  },
  methods: {
    showForm(){
      //Logic 
      this.form = !this.form
    },
    
    submitForm() {
    if(localStorage.getItem("jwt")){
        const user = JSON.parse(localStorage.getItem("user"))
      fetch("https://lyf-styl-reservation.herokuapp.com/booking", {
        method: "POST",
        headers: { "Content-type": "application/json; charset=UTF-8", 
        Authorization: `Bearer ${localStorage.getItem("jwt")}` },

        body: JSON.stringify({
            email: user.email,
            firstname: user.firstname,
          people: this.people,
          number: this.number,
          hours: this.hours,
          days: this.days,
        }),
      })
        .then((response) => response.json())
        .then((json) => {
          console.log(json);
        })
        .catch((err) => console.log(err));
    }
    },
  },
  mounted(){
        if (!localStorage.getItem("jwt")) {
            alert("User not logged in");
            
        }
      },
}
</script>

<style scoped>
#banner{
    min-height: 100vh;
    background: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), url("../assets/banner-img.jpg") center/cover no-repeat;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    color: #fff;
    padding-bottom: 20px;
}
.card-container{
    /* display: grid; */
    grid-template-columns: 420px 520px;
}
.card-img{
    background: url("../assets/login-banner.jpeg") center/cover no-repeat;
}
.banner h2{
    padding-bottom: 40px;
    margin-bottom: 20px;
}
.card-content{
    background: #fff;
    height: 330px;
}
.card-content h3{
    text-align: center;
    color: #000;
    padding: 25px 0 10px 0;
    font-size: 26px;
    font-weight: 500;
}
.form-row{
    display: flex;
    width: 90%;
    margin: 0 auto;
}
form select, form input{
    display: block;
    width: 100%;
    margin: 15px 12px;
    padding: 5px;
    font-size: 15px;
    /* font-family: 'Poppins', sans-serif; */
    outline: none;
    border: none;
    border-bottom: 1px solid #eee;
    font-weight: 300;
}
form input[type = text], form input[type = number], form input::placeholder, select{
    color: #9a9a9a;
}
form input[type = submit]{
    color: #fff;
    background: var(--persian-red);
    padding: 12px 0;
    border-radius: 4px;
    cursor: pointer;
}
form input[type = submit]:hover{
    background-color: var(--dark);
}
@media(max-width: 992px){
    .card-container{
        grid-template-columns: 100%;
        width: 100vw;
    }
    .card-img{
        height: 330px;
    }
}
</style>

