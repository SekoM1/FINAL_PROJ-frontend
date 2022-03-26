<template>
  <!-- nabar -->
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container-fluid">
      <a href="index.html" class="navbar-brand">LYF <span>.</span> STYL</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0 mx-auto">
          <li class="nav-item">
            <a @click="hideBooking" href="#home" class="nav-link">HOME</a>
          </li>
          <li class="nav-item">
            <a @click="hideBooking" href="#about" class="nav-link">ABOUT</a>
          </li>
          <li class="nav-item">
            <a @click="hideBooking" href="#chef" class="nav-link">CHEFS</a>
          </li>
          <li class="nav-item">
            <a @click="hideBooking" href="#menu" class="nav-link">MENU</a>
          </li>
          <li class="nav-item">
            <a @click="hideBooking" href="#contact" class="nav-link">CONTACT</a>
          </li>
        </ul>

        <!-- Button trigger modal -->
        <button
          type="button"
          class="btn btn-outline"
          data-bs-toggle="modal"
          data-bs-target="#exampleModal"
        >
          Login
        </button>

        <!-- logout button -->

        <button
          type="submit"
          id="logout"
          class="btn btn-outline"
          @click="logout"
        >
          Log out
        </button>

        <!-- Modal -->
        <div
          class="modal fade"
          id="exampleModal"
          tabindex="-1"
          aria-labelledby="exampleModalLabel"
          aria-hidden="true"
        >
          <div class="modal-dialog">
            <div class="modal-content">
              <div class="modal-header">
                <h5 class="modal-title" id="exampleModalLabel">LOGIN</h5>
                <button
                  type="button"
                  class="btn-close"
                  data-bs-dismiss="modal"
                  aria-label="Close"
                ></button>
              </div>
              <div class="modal-body">
                <form @submit.prevent="login">
                  <div class="group log-input">
                    <input
                      type="email"
                      id="email"
                      v-model="email"
                      placeholder="Email"
                    />
                  </div>

                  <div class="group log-input">
                    <input
                      type="password"
                      id="password"
                      v-model="password"
                      placeholder="Password"
                    />
                  </div>

                  <span class="check left-align">
                    <input type="checkbox" />
                    <label>Remember Me</label>
                  </span>

                  <br /><br />
                  <!-- login btn -->
                  <div class="modal-footer">
                    <button
                      type="submit"
                      class="btn btn-outline"
                      data-bs-dismiss="modal"
                    >
                      Login
                    </button>
                    <!-- sign up btn -->
                    <button
                      type="button"
                      class="btn btn-outline"
                      data-bs-dismiss="modal"
                      data-bs-toggle="modal"
                      data-bs-target="#exampleModal1"
                    >
                      Sign up
                    </button>
                  </div>
                </form>
              </div>
            </div>
          </div>
        </div>

        <!-- Modal -->
        <div
          class="modal fade"
          id="exampleModal1"
          tabindex="-1"
          aria-labelledby="exampleModalLabel"
          aria-hidden="true"
        >
          <div class="modal-dialog">
            <div class="modal-content">
              <div class="modal-header">
                <h5 class="modal-title" id="exampleModalLabel1">SIGN UP</h5>
                <button
                  type="button"
                  class="btn-close"
                  data-bs-dismiss="modal"
                  aria-label="Close"
                ></button>
              </div>
              <div class="modal-body">
                <!-- body of form -->
                <form @submit.prevent="register">
                  <div class="group log-input">
                    <input
                      type="text"
                      id="firstname"
                      v-model="firstname"
                      placeholder="First Name"
                    />
                  </div>

                  <div class="group log-input">
                    <input
                      type="text"
                      id="lastname"
                      v-model="lastname"
                      placeholder="Last Name"
                    />
                  </div>

                  <div class="group log-input">
                    <input
                      type="email"
                      id="email"
                      v-model="email"
                      placeholder="Email address"
                    />
                  </div>

                  <div class="group log-input">
                    <input
                      type="password"
                      id="password"
                      v-model="password"
                      placeholder="Password"
                    />
                  </div>

                  <span class="check left-align">
                    <input type="checkbox" />
                    <label>Remember Me</label>
                  </span>

                  <!-- <a class = "right-align" href="#">Forgot Password</a> -->

                  <br /><br />
                  <div class="modal-footer">
                    <button
                      type="submit"
                      class="btn btn-secondary"
                      data-bs-dismiss="modal"
                    >
                      Sign in
                    </button>
                  </div>
                </form>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  methods: {
    hideBooking: function () {
      this.$emit("changePage", false);
    },
  },

  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    logout() {
    console.log("user logged out")
    localStorage.clear();
    alert("logged out");
  },
    login() {
      fetch("https://lyf-styl-reservation.herokuapp.com/users/login", {
        method: "PATCH",
        body: JSON.stringify({
          email: this.email,
          password: this.password,
        }),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
        },
      })
        .then((response) => response.json())
        .then(async(json) => {
          if(json.jwt){
                        console.log(json.jwt)
                          localStorage.setItem("jwt", json.jwt);
          localStorage.setItem("user", JSON.stringify(json.user))
          console.log(json.jwt);
          console.log(json.user)
            alert("User logged in");
            return await localStorage.setItem("jwt", json.jwt);
          
          }
          console.log(json);
          alert("Wrong Credentials")
        }
        
        )

        
        .catch((err) => {
          alert(err);
          this.loading = false
        });
    },

    register() {
      const newUser = {
        firstname: this.firstname,
        lastname: this.lastname,
        email: this.email,
        password: this.password,
      };
      fetch("https://lyf-styl-reservation.herokuapp.com/users/register", {
        method: "POST",
        body: JSON.stringify(newUser),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
        },
      })
        .then((response) => response.json())
        .then((json) => {
          console.log(json);
          localStorage.setItem("jwt", json.jwt);
          alert("NEW User registered");
          // this.$router.push({ name: "Home" });
        })
        .catch((err) => {
          alert(err);
        });
    },
  },

  
};
</script>

<style >
/* modal */
#logout {
  margin-left: 10px;
}

#logout[disabled] {
  background-color: lightgray;
  color: gray;
}

.group {
  position: relative;
  margin-bottom: 45px;
}

.log-input {
  font-size: 18px;
  padding: 10px 10px 10px 5px;
  -webkit-appearance: none;
  display: block;

  color: #636363;
  width: 100%;
  border-bottom: 1px solid #757575;
}

.log-input:focus {
  outline: none;
}

.log-form a {
  font-size: 9px;
  font-weight: 600;
  letter-spacing: 0.3em;
  line-height: 24px;
  text-transform: uppercase;
  color: #aaaaaa;
}

.left-align {
  float: left;
  text-align: left;
}

.right-align {
  float: right;
  text-align: right;
}
input {
  border: none;
}
.modal-footer {
  border: none;
}
input:focus {
  outline: none;
}
.modal-content {
  margin-top: 250px;
}
.modal-header {
  display: flex;
  flex-shrink: 0;
  align-items: center;
  justify-content: space-between;
  padding: 1rem 1rem;
  border-bottom: 1px solid #dee2e6;
  border-top-left-radius: calc(0.3rem - 1px);
  border-top-right-radius: calc(0.3rem - 1px);
}

/* modalend */
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 999;
  width: 100% !important;
  padding-left: 5vw;
  padding-right: 5vw;
  background: rgb(241, 240, 240);
}
.navbar-brand {
  font-weight: 700;
}
.navbar-light .navbar-nav .nav-link {
  color: var(--grey);
  font-weight: 700;
}
.navbar-light .navbar-nav .nav-link:hover {
  color: var(--persian-red);
}
.navbar-brand span {
  color: var(--persian-red);
}
.navbar-toggler:hover {
  color: var(--persian-red);
}

li .nav-item {
  margin-left: 35%;
}
</style>
