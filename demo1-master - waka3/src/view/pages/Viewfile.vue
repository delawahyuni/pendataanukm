<template>
  <!--begin::Mixed Widget 1-->

  <div class="card card-custom bg-gray-100 card-stretch gutter-b">
    <!--begin::Header-->
    <b-container class="bv-example-row bv-example-row-flex-cols">
      <b-row>
        <b-col align-self="center">
          <template>
            <v-data-table
              :headers="headers"
              :items="desserts"
              sort-by="calories"
              class="elevation-1"
            >
              <template v-slot:top>
                <v-toolbar flat>
                  <v-toolbar-title>Data Laporan Pengajuan </v-toolbar-title>
                  <br />
                  <div>
              
                  </div>
                  <v-dialog v-model="dialogDelete" max-width="500px">
                    <v-card>
                      <v-card-title class="text-h5"
                        >Are you sure you want to delete this
                        item?</v-card-title
                      >
                      <v-card-actions>
                        <v-spacer></v-spacer>
                        <v-spacer></v-spacer>
                      </v-card-actions>
                    </v-card>
                  </v-dialog>
                </v-toolbar>
              </template>
              <template v-slot:[`item.actions`]="{ item }">
                <v-btn class="">
                  <router-link to="#" v-slot="{ href, navigate }">
                    <a :href="href" class="menu-link" @click="navigate">
                      {{ value }}
                      <v-icon>
                        mdi-folder-download
                      </v-icon>
                    </a>
                  </router-link>
                </v-btn>
                <v-icon small @click="deleteItem(item)"> </v-icon>
              </template>
              <template v-slot:no-data>
                <v-btn color="primary" @click="initialize">
                  Reset
                </v-btn>
              </template>
            </v-data-table>
          </template>
        </b-col>
      </b-row>
    </b-container>
    <!--end::Header-->
    <!--begin::Body-->
    <!--end::Mixed Widget 1-->
  </div>
</template>
<script>
// import KTCodePreview from "@/view/content/CodePreview.vue";
import { SET_BREADCRUMB } from "@/core/services/store/breadcrumbs.module";
export default {
  name: "datapembayaranmahasiswa",
  components: {
    // KTCodePreview
  },
  data: () => ({
    dialog: false,
    dialogDelete: false,
    headers: [
      {
        text: "Nama UKM",
        align: "nama",
        sortable: false,
        value: "nama"
      },
      {
        text: "Bulan",
        value: "bulan"
      },
      {
        text: "Jenis Kegiatan",
        value: "kegiatan"
      },
      {
        text: "Jenis File",
        value: "file"
      },
      {
        text: "Actions",
        value: "actions",
        sortable: false
      }
    ],
    desserts: [],
    editedIndex: -1,
    editedItem: {
      name: "",
      calories: 0,
      fat: 0,
      carbs: 0,
      protein: 0
    },
    defaultItem: {
      name: "",
      calories: 0,
      fat: 0,
      carbs: 0,
      protein: 0
    }
  }),
  mounted() {
    this.$store.dispatch(SET_BREADCRUMB, [
      {
        title: "Vue Bootstrap",
        route: "alert"
      },
      {
        title: ""
      }
    ]);
  },

  computed: {
    formTitle() {
      return this.editedIndex === -1 ? "New Item" : "Edit Item";
    }
  },

  watch: {
    dialog(val) {
      val || this.close();
    },
    dialogDelete(val) {
      val || this.closeDelete();
    }
  },

  created() {
    this.initialize();
  },

  methods: {
    initialize() {
      this.desserts = [
        {
          syarat: "nama",
          dokumen: "UKM Dance",
        },
        {
          syarat: "Rekap Nilai",
          dokumen: "Rekap Nilai.pdf",
        },
        {
          syarat: "KK",
          dokumen: "KK.pdf",
        },
        {
          syarat: "KK",
          dokumen: "KK.pdf",
        },
        {
         syarat: "Rekap Nilai",
          dokumen: "Rekap Nilai.pdf",
        }
      ];
    },

    editItem(item) {
      this.editedIndex = this.desserts.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialog = true;
    },

    deleteItem(item) {
      this.editedIndex = this.desserts.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialogDelete = true;
    },

    deleteItemConfirm() {
      this.desserts.splice(this.editedIndex, 1);
      this.closeDelete();
    },

    close() {
      this.dialog = false;
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      });
    },

    closeDelete() {
      this.dialogDelete = false;
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      });
    },

    save() {
      if (this.editedIndex > -1) {
        Object.assign(this.desserts[this.editedIndex], this.editedItem);
      } else {
        this.desserts.push(this.editedItem);
      }
      this.close();
    }
  }
};
</script>