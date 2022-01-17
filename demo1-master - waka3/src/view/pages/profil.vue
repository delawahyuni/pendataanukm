<template>
  <div>
    <!--begin::Dashboard-->
    <div class="row">
      <div class="col-md-12">

        <KTCodePreview v-bind:title="'Unit Kegiatan Mahasiswa STMIK Primakara'">
          <template v-slot:preview>
            <div>
              <b-button to="/addukm" variant="primary">Add UKM</b-button>
            </div>
            <br>
            <div>
              <b-card-group deck>
                <b-card header-tag="header" footer="" footer-tag="footer" title="">
                  <template v-slot:header>
                    <h6 class="mb-0">UKM DANCE</h6>
                  </template>
                  <b-card-text>Punya hobby menari? Salurkan bakat menarimu dengan bergabung di UKM Dance Primakara. Kamu
                    dapat mempelajari tari modern maupun tari tradisional di UKM ini lohh.</b-card-text>
                  <b-button to="/ukmdance" variant="primary">See More</b-button>
                </b-card>

                <b-card title="" header-tag="header" footer-tag="footer">
                  <template v-slot:header>
                    <h6 class="mb-0">UKM MUSIK </h6>
                  </template>
                  <b-card-text>Salah satu UKM yang ada di Primakara adalah UKM Musik. Bagi kalian yang ingin
                    mengembangkan bakat musik, kami menyediakan studio musik agar lebih mudah untuk berkreasi.
                  </b-card-text>
                  <b-button to="/ukmmusik" variant="primary">See More</b-button>
                  <template v-slot:footer>
                    <!--<em>Footer Slot</em-->
                  </template>
                </b-card>
              </b-card-group>
              <b-card-group deck>
                <b-card header-tag="header" footer="" footer-tag="footer" title="">
                  <template v-slot:header>
                    <h6 class="mb-0">UKM MAPALA</h6>
                  </template>
                  <b-card-text>UKM Mapala adalah perkumpulan Mahasiswa Pecinta Alam dengan kegiatan rutin di alam
                    terbuka seperti pendakian gunung dan menanam seribu pohon.</b-card-text>
                  <b-button to="/ukmmapala" variant="primary">See More</b-button>
                </b-card>

                <b-card title="" header-tag="header" footer-tag="footer">
                  <template v-slot:header>
                    <h6 class="mb-0">UKM ESPRIME</h6>
                  </template>
                  <b-card-text>Buat kalian yang suka main game, cocok banget nih buat gabung di UKM Esprime. Kalian bisa
                    membentuk dan menggembleng diri bersama UKM Esprime melalui berbagai turnamen Offline dan Online
                    yang diadakan.</b-card-text>
                  <b-button to="/ukmesprime" variant="primary">See More</b-button>
                  <template v-slot:footer>
                    <!--<em>Footer Slot</em-->
                  </template>
                </b-card>
              </b-card-group>
            </div>
          </template>
          <template v-slot:code>
            <highlight-code lang="html">
              {{ html5 }}
            </highlight-code>
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
        html5: `<div>
<b-card-group deck>
  <b-card
    header="featured"
    header-tag="header"
    footer="Card Footer"
    footer-tag="footer"
    title="Title"
  >
    <b-card-text>Header and footers using props.</b-card-text>
    <b-button href="#" variant="primary">Go somewhere</b-button>
  </b-card>

  <b-card title="Title" header-tag="header" footer-tag="footer">
    <template v-slot:header>
      <h6 class="mb-0">Header Slot</h6>
    </template>
    <b-card-text>Header and footers using slots.</b-card-text>
    <b-button href="#" variant="primary">Go somewhere</b-button>
    <template v-slot:footer>
      <em>Footer Slot</em>
    </template>
  </b-card>
</b-card-group>
</div>`,

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