<template>
  <div class="login">
    <b-field label="Username"
            type="is-success"
            message="This username is available">
            <b-input v-model="username"></b-input>
        </b-field>

        <b-field label="Password">
            <b-input type="password"
                v-model="password"
                password-reveal>
            </b-input>
        </b-field>  

    <br/>
    <button class="button is-danger" @click="handleLogin">Log In</button>
  </div>
</template>

<script>
export default {
    name: "Login",
    data: function() {
        return {
            username: "",
            password: "",
        };
    },
    methods: {
        handleLogin: function() {
            fetch(`${this.$route.query.URL}/auth/users/login/`, {
                method: "post",
                headers: {
                    "Content-Type": "application/json",
                },
                body: JSON.stringify({
                    username: this.username,
                    password: this.password,
                }),
            })
            .then(response => 
            {
                if (response.status !== 200) {
                    response.json()
                } else {
                    return response.json()
                }
            }
            )
            .then(data => {
                console.log(data)
                if (data) {
                this.$emit('loggedIn', data)
                } else {
                    alert('In correct login')
                }
            });
        },
    },
};
</script>