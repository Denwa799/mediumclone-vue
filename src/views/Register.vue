<template>
    <div class="auth-page">
        <div class="container page">
            <div class="row">
                <div class="col-md-6 offset-md-3 col-xs-12">
                    <h1 class="text-xs-center">Sign Up</h1>
                    <p class="text-xs-center">
                        <router-link :to="{ name: 'login' }">
                            Nave an account?
                        </router-link>
                    </p>
                    <app-validation-errors v-if="validationErrors" :validation-errors="validationErrors" />
                    <form @submit.prevent="onSubmit">
                        <fieldset class="form-group">
                            <input class="form-control form-control-lg" type="text" placeholder="Username"
                                v-model="username" />
                        </fieldset>
                        <fieldset class="form-group">
                            <input class="form-control form-control-lg" type="text" placeholder="Email"
                                v-model="email" />
                        </fieldset>
                        <fieldset class="form-group">
                            <input class="form-control form-control-lg" type="password" placeholder="Password"
                                v-model="password" />
                        </fieldset>
                        <button class="btn btn-lg btn-primary pull-xs-right" :disabled="isSubmitting">
                            Sign Up
                        </button>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { mapGetters } from 'vuex'
import { getterTypes } from '@/store/modules/auth'
import AppValidationErrors from '@/components/ValidationErrors.vue'
import { actionTypes } from '@/store/modules/auth'

export default {
    name: 'AppRegister',
    components: {
        AppValidationErrors
    },
    data() {
        return {
            email: '',
            password: '',
            username: ''
        }
    },
    computed: {
        ...mapGetters({
            isSubmitting: getterTypes.isSubmitting,
            validationErrors: getterTypes.validationErrors,
        })
    },
    methods: {
        onSubmit() {
            this.$store.dispatch(actionTypes.register, {
                email: this.email,
                password: this.password,
                username: this.username
            })
                .then(() => {
                    this.$router.push({ name: 'globalFeed' })
                })
        },
    }
}
</script>