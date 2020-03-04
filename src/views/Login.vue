<template>
  <form class="form-signin" @submit.prevent="login">

    <div class="form-label-group">
      <input
        type="email"
        id="inputEmail"
        class="form-control"
        placeholder="Email address"
        required
        autofocus
        v-model="email"
      />
      <label for="inputEmail">Email address</label>
    </div>

    <div class="form-label-group">
      <input
        type="password"
        id="inputPassword"
        class="form-control"
        placeholder="Password"
        required
        v-model="password"
      />
      <label for="inputPassword">Password</label>
    </div>

    <div class="form-group">
      <span v-if="error" class="text-danger">{{error}}</span>  
    </div>

    <button class="btn btn-lg btn-primary btn-block" type="submit">Sign in</button>
  </form>
</template>

<script>
import axios from "../plugins/axios";

export default {
  data() {
    return {
      user: {},
      email: "john@email.com",
      password: "password",
      error: null
    };
  },
  methods: {
    login() {
      axios.get("/airlock/csrf-cookie").then(() => {
        axios
          .post("/api/login", {
            email: this.email,
            password: this.password
          })
          .then(() => {
            localStorage.setItem("isLogged", true);
            this.$router.push({ name: "Home" });
          })
          .catch(error => {
            const errors = error.response.data.errors;
            const key = Object.keys(errors)[0];
            this.error = errors[key][0];
          });
      });
    }
  }
};
</script>

<style>
.form-label-group {
  position: relative;
  margin-bottom: 1rem;
}

.form-label-group > input,
.form-label-group > label {
  height: 3.125rem;
  padding: 0.75rem;
}

.form-label-group > label {
  position: absolute;
  top: 0;
  left: 0;
  display: block;
  width: 100%;
  margin-bottom: 0; /* Override default `<label>` margin */
  line-height: 1.5;
  color: #495057;
  pointer-events: none;
  cursor: text; /* Match the input under the label */
  border: 1px solid transparent;
  border-radius: 0.25rem;
  transition: all 0.1s ease-in-out;
}

.form-label-group input::-webkit-input-placeholder {
  color: transparent;
}

.form-label-group input:-ms-input-placeholder {
  color: transparent;
}

.form-label-group input::-ms-input-placeholder {
  color: transparent;
}

.form-label-group input::-moz-placeholder {
  color: transparent;
}

.form-label-group input::placeholder {
  color: transparent;
}

.form-label-group input:not(:placeholder-shown) {
  padding-top: 1.25rem;
  padding-bottom: 0.25rem;
}

.form-label-group input:not(:placeholder-shown) ~ label {
  padding-top: 0.25rem;
  padding-bottom: 0.25rem;
  font-size: 12px;
  color: #777;
}

/* Fallback for Edge
-------------------------------------------------- */
@supports (-ms-ime-align: auto) {
  .form-label-group > label {
    display: none;
  }
  .form-label-group input::-ms-input-placeholder {
    color: #777;
  }
}

/* Fallback for IE
-------------------------------------------------- */
@media all and (-ms-high-contrast: none), (-ms-high-contrast: active) {
  .form-label-group > label {
    display: none;
  }
  .form-label-group input:-ms-input-placeholder {
    color: #777;
  }
}
</style>