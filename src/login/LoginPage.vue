<template>
    <div>
        <h2>Welcome, please login.</h2>
        <form @submit.prevent="handleSubmit">
            <div class="form-group">
                <label for="userName">Username</label>
                <input type="text" v-model="userName" name="userName" class="form-control" :class="{ 'is-invalid': submitted && !username }" />
                <div v-show="submitted && !userName" class="invalid-feedback">Username is required</div>
            </div>
            <div class="form-group">
                <label htmlFor="password">Password</label>
                <input type="password" v-model="password" name="password" class="form-control" :class="{ 'is-invalid': submitted && !password }" />
                <div v-show="submitted && !password" class="invalid-feedback">Password is required</div>
            </div>
            <div class="form-group">
                <button class="btn btn-info" :disabled="status.loggingIn">Sign in</button>
                <router-link to="/register" class="btn btn-outline-danger">Sign up</router-link>
            </div>
        </form>
    </div>
</template>

<script>
import { mapState, mapActions } from 'vuex'

export default {
    data () {
        return {
            userName: '',
            password: '',
            submitted: false
        }
    },
    computed: {
        ...mapState('account', ['status'])
    },
    created () {
        this.logout();
    },
    methods: {
        ...mapActions('account', ['login', 'logout']),
        handleSubmit (e) {
            this.submitted = true;
            const { userName, password } = this;
            if (userName && password) {
                this.login({ userName, password })
            }
        }
    }
};
</script>