<template>
    <div>
        <!--begin::Dashboard-->
        <div class="row">
            <div class="col-md-12">
                <KTCodePreview v-bind:title="'Upload Event Poster'">
                    <template v-slot:preview>
                        <h4>
                            Unit Kegiatan Mahasiswa
                            STMIK Primakara
                        </h4>
                        <br>
                        <div>
                            <b-form @submit="onSubmit" @reset="onReset" v-if="show">

                                <b-form-group id="input-group-2" label="Nama UKM:" label-for="input-2">
                                    <b-form-input id="input-2" v-model="form.name" required placeholder="Enter UKM">
                                    </b-form-input>
                                </b-form-group>
                                <b-form-group label="Upload Poster:" label-cols-sm="2">
                                    <b-form-file id="file-default"></b-form-file>
                                </b-form-group>
                                <b-form-group id="input-group-2" label="Caption:" label-for="input-2">
                                    <b-form-input id="input-2" v-model="form.name" required placeholder="Enter Caption">
                                    </b-form-input>
                                </b-form-group>

                                <center>

                                    <v-btn :loading="loading3" :disabled="loading3" color="blue-grey"
                                        class="ma-2 white--text" @click="loader = 'loading3'">
                                        Submit
                                        <v-icon right dark>mdi-cloud-upload</v-icon>
                                    </v-btn>
                                </center>
                            </b-form>
                        </div>
                    </template>
                    <template v-slot:html>
                        {{ html1 }}
                    </template>
                    <template v-slot:js>
                        {{ js1 }}
                    </template>
                </KTCodePreview>
            </div>
        </div>
        <!--end::Dashboard-->
    </div>
</template>

<script>
    import KTCodePreview from "@/view/content/CodePreview.vue";
    import {
        SET_BREADCRUMB
    } from "@/core/services/store/breadcrumbs.module";

    export default {
        data() {
            return {

                html1: `<div>
    <b-form @submit="onSubmit" @reset="onReset" v-if="show">
      <b-form-group
        id="input-group-1"
        label="Email address:"
        label-for="input-1"
        description="We'll never share your email with anyone else."
      >
        <b-form-input
          id="input-1"
          v-model="form.email"
          type="email"
          required
          placeholder="Enter email"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Your Name:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="form.name"
          required
          placeholder="Enter name"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-3" label="Food:" label-for="input-3">
        <b-form-select
          id="input-3"
          v-model="form.food"
          :options="foods"
          required
        ></b-form-select>
      </b-form-group>

      <b-form-group id="input-group-4">
        <b-form-checkbox-group v-model="form.checked" id="checkboxes-4">
          <b-form-checkbox value="me">Check me out</b-form-checkbox>
          <b-form-checkbox value="that">Check that out</b-form-checkbox>
        </b-form-checkbox-group>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
    <b-card class="mt-3" header="Form Data Result">
      <pre class="m-0">{{ form }}</pre>
    </b-card>
  </div>`,
                js1: `
  export default {
    data() {
      return {
        form: {
          email: '',
          name: '',
          food: null,
          checked: []
        },
        foods: [{ text: 'Select One', value: null }, 'Carrots', 'Beans', 'Tomatoes', 'Corn'],
        show: true
      }
    },
    methods: {
      onSubmit(evt) {
        evt.preventDefault()
        alert(JSON.stringify(this.form))
      },
      onReset(evt) {
        evt.preventDefault()
        // Reset our form values
        this.form.email = ''
        this.form.name = ''
        this.form.food = null
        this.form.checked = []
        // Trick to reset/clear native browser form validation state
        this.show = false
        this.$nextTick(() => {
          this.show = true
        })
      }
    }
  }`,
                form: {
                    email: "",
                    name: "",
                    food: null,
                    checked: []
                },
                foods: [{
                        text: "Select One",
                        value: null
                    },
                    "Carrots",
                    "Beans",
                    "Tomatoes",
                    "Corn"
                ],
                show: true,
            };
        },
        name: "profil",
        components: {
            KTCodePreview
        },
        mounted() {
            this.$store.dispatch(SET_BREADCRUMB, [{
                title: "Profil"
            }]);
        },
        methods: {
            setActiveTab1(event) {
                this.tabIndex = this.setActiveTab(event);
            },
            setActiveTab2(event) {
                this.tabIndex2 = this.setActiveTab(event);
            },
            /**
             * Set current active on click
             * @param event
             */
            setActiveTab(event) {
                // get all tab links
                const tab = event.target.closest('[role="tablist"]');
                const links = tab.querySelectorAll(".nav-link");
                // remove active tab links
                for (let i = 0; i < links.length; i++) {
                    links[i].classList.remove("active");
                }

                // set current active tab
                event.target.classList.add("active");

                // set clicked tab index to bootstrap tab
                return parseInt(event.target.getAttribute("data-tab"));
            }
        }
    };
</script>