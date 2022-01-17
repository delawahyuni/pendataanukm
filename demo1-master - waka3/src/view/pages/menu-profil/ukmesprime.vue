<template>
  <div>
    <!--begin::Dashboard-->
    <div class="row">
      <div class="col-md-12">
        <KTCodePreview v-bind:title="'UKM ESPRIME'">
          <template v-slot:preview>
            <div>
              <b-card title="Profil" sub-title="">
                <b-card-img
                  src="media/svg/image/logoukm/logoukmesprime.jpeg"
                  class="rounded-0"
                  style="height: 180px; width: 180px"
                ></b-card-img>
                <b-card-text>
                  Punya hobby bermain game? Salurkan bakat bermainmu dengan
                  bergabung di UKM Esprime Primakara. Kamu dapat keseruan
                  sekaligus hal yang positif dengan mengikuti kejuaraan game di
                  UKM ini lo.
                  <ul>
                    <li>Kegiatan UKM Esprime:</li>
                  <ol>
                    <li>Mengikuti Turnament</li>
                    <li>StartupDay</li>
                  </ol>
                  </ul>
                  <ul>
                    <li>Pembina : A. A Siva Larasanti, S.Kom</li>
                    <li>Ketua :Ferry Ari Wijaya</li>
                    <li>Contact Person : Ferry +62 895-4133-14956</li>
                    <li>
                      Link Pendaftaran :bit.ly/RecruitmentAnggotaUKMDancePrimakara2021
                    </li>
                  </ul>
                </b-card-text>
                <b-button to="/ukmesprime" variant="outline-primary"
                  >Edit Text</b-button
                >
              </b-card>
            </div>
          </template>
          <template v-slot:code>
            <highlight-code lang="html">
              {{ html4 }}
            </highlight-code>
          </template>
        </KTCodePreview>
      </div>
      <div class="col-md-12">
        <KTCodePreview v-bind:title="'Galeri UKM ESPRIME'">
          <template v-slot:preview>
    
            <b-container fluid class="p-4 bg-dark">
              <b-row>
                <b-col>
                  <b-img
                    thumbnail
                    fluid
                    src="https://picsum.photos/250/250/?image=54"
                    alt="Image 1"
                  ></b-img>
                </b-col>
                <b-col>
                  <b-img
                    thumbnail
                    fluid
                    src="https://picsum.photos/250/250/?image=58"
                    alt="Image 2"
                  ></b-img>
                </b-col>
                <b-col>
                  <b-img
                    thumbnail
                    fluid
                    src="https://picsum.photos/250/250/?image=59"
                    alt="Image 3"
                  ></b-img>
                </b-col>
              </b-row>
            </b-container>
            <b-container fluid class="p-4 bg-dark">
              <b-row>
                <b-col>
                  <b-img
                    thumbnail
                    fluid
                    src="https://picsum.photos/250/250/?image=54"
                    alt="Image 1"
                  ></b-img>
                </b-col>
                <b-col>
                  <b-img
                    thumbnail
                    fluid
                    src="https://picsum.photos/250/250/?image=58"
                    alt="Image 2"
                  ></b-img>
                </b-col>
                <b-col>
                  <b-img
                    thumbnail
                    fluid
                    src="https://picsum.photos/250/250/?image=59"
                    alt="Image 3"
                  ></b-img>
                </b-col>
              </b-row>
            </b-container>
            <b-container fluid class="">
              <b-button to="/ukmesprime" variant="outline-info"
                >Upload</b-button
              >
            </b-container>
          </template>
          <template v-slot:html>
            {{ code3.html }}
          </template>
        </KTCodePreview>
      </div>
    </div>
    <!--end::Dashboard-->
  </div>
</template>

<script>
import KTCodePreview from "@/view/content/CodePreview.vue";
import { SET_BREADCRUMB } from "@/core/services/store/breadcrumbs.module";

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
      code3: {
        html: `<b-container fluid class="p-4 bg-dark">
  <b-row>
    <b-col>
      <b-img thumbnail fluid src="https://picsum.photos/250/250/?image=54" alt="Image 1"></b-img>
    </b-col>
    <b-col>
      <b-img thumbnail fluid src="https://picsum.photos/250/250/?image=58" alt="Image 2"></b-img>
    </b-col>
    <b-col>
      <b-img thumbnail fluid src="https://picsum.photos/250/250/?image=59" alt="Image 3"></b-img>
    </b-col>
  </b-row>
</b-container>`,
      },
    };
  },
  name: "profil",
  components: {
    KTCodePreview,
  },
  mounted() {
    this.$store.dispatch(SET_BREADCRUMB, [
      {
        title: "Profil",
      },
    ]);
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
    },
  },
};
</script>