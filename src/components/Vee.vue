<template>
    <div class="card">
    <h3 class="card-header text-center">Vee Validate Form</h3>
    <ValidationObserver v-slot="{ handleSubmit }">
        <form @submit.prevent="handleSubmit(onSubmit)">
        <div>
            <div class="card-body">
                <ValidationProvider
                    name="Name"
                    rules="required|alpha"
                    v-slot="{ errors }"
                >
                    <div class="form-group">
                    <label>Name</label>
                    <input class="form-control" v-model="formData.name" />
                    <span class="error">{{ errors[0] }}</span>
                    </div>
                </ValidationProvider>

                <ValidationProvider
                    name="E-mail"
                    rules="required|email"
                    v-slot="{ errors }"
                >
                    <div class="form-group">
                    <label>Email</label>
                    <input class="form-control" v-model="formData.email" type="email" />
                    <span class="error">{{ errors[0] }}</span>
                    </div>
                </ValidationProvider>

                <ValidationProvider
                    name="Password"
                    rules="required|min:6|max:12"
                    v-slot="{ errors }"
                >
                    <div class="form-group">
                    <label>Password</label>
                    <input
                        class="form-control"
                        v-model="formData.password"
                        type="password"
                    />
                    <span class="error">{{ errors[0] }}</span>
                    </div>
                </ValidationProvider>

                <ValidationProvider name="Gender" rules="required" v-slot="{ errors }">
                    <div class="form-group">
                    <label>Gender</label>
                    <select class="form-control" v-model="formData.gender">
                        <option value="male">Male</option>
                        <option value="female">Female</option>
                        <option value="other">Other</option>
                    </select>
                    <span class="error">{{ errors[0] }}</span>
                    </div>
                </ValidationProvider>
                <ValidationProvider
                    name="AcceptTerms"
                    rules="required"
                    v-slot="{ errors }"
                >
                    <div class="form-check">
                    <input
                        class="form-check-input"
                        type="checkbox"
                        v-model="formData.acceptTerms"
                    />
                    <label class="form-check-label">Accept Terms </label>
                    <span class="error">{{ errors[0] }}</span>
                    </div>
                </ValidationProvider>
                <input class="btn btn-primary mt-2" type="submit" text="submit" />
            </div>
        </div>
        </form>
    </ValidationObserver>
    </div>
</template>

<script>
export default {
  data: () => ({
    formData: {
      name: '',
      email: '',
      password: '',
      gender: '',
      acceptTerms: null,
    },
  }),
  methods: {
    onSubmit() {
      console.log(this.formData);
    },
  },
};
</script>

<style>
.card-body {
  text-align:start;
}
.error {
    color: red;
}
</style>
