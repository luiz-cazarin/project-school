<template>
  <div class="test pa-6">
    <v-data-table
      :headers="headers"
      :items="tests"
      sort-by="situation"
      class="elevation-1"
    >
      <template v-slot:top>
        <v-toolbar flat>
          <v-toolbar-title>Avaliacoes</v-toolbar-title>

          <v-spacer></v-spacer>
          <v-dialog v-model="dialog" max-width="500px">
            <template v-slot:activator="{ on, attrs }">
              <v-btn color="primary" dark class="mb-2" v-bind="attrs" v-on="on">
                Nova Prova
              </v-btn>
            </template>
            <v-card>
              <v-card-title>
                <span class="text-h5">{{ formTitle }}</span>
              </v-card-title>
              <v-card-text>
                <v-container>
                  <v-row>
                    <v-col cols="12" sm="20" md="20">
                      <v-text-field
                        v-model="editedItem.name"
                        label="Materia"
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="5">
                      <v-text-field
                        v-model="editedItem.situation"
                        label="Situacao"
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="5">
                      <v-text-field
                        v-model="editedItem.grade"
                        label="Nota/Conceito"
                      ></v-text-field>
                    </v-col>
                  </v-row>
                </v-container>
              </v-card-text>

              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="blue darken-1" text @click="close">
                  Cancelar
                </v-btn>
                <v-btn color="blue darken-1" text @click="save"> Salvar </v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog>
          <v-dialog v-model="dialogDelete" max-width="500px">
            <v-card>
              <v-card-title class="text-h6"
                >Tem certeza de que quer excluir este aluno?</v-card-title
              >
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="blue darken-1" text @click="closeDelete"
                  >Cancel</v-btn
                >
                <v-btn color="blue darken-1" text @click="deleteItemConfirm"
                  >OK</v-btn
                >
                <v-spacer></v-spacer>
              </v-card-actions>
            </v-card>
          </v-dialog>
        </v-toolbar>
      </template>

      <template v-slot:item.actions="{ item }">
        <v-icon small class="mr-2" @click="editItem(item)"> mdi-pencil </v-icon>
        <v-icon small @click="deleteItem(item)"> mdi-delete </v-icon>
      </template>
      <template v-slot:no-data>
        <v-btn color="primary" @click="initialize"> Reset </v-btn>
      </template>
    </v-data-table>
  </div>
</template>





<script>
export default {
  data: () => ({
    dialog: false,
    dialogDelete: false,
    headers: [
      { text: "Materia", value: "name" },
      { text: "Situacao", value: "situation" },
      { text: "Nota/Conceito", value: "grade" },
      { text: "Acoes", value: "actions", sortable: false },
    ],
    tests: [],
    editedIndex: -1,
    situation: "",
    editedItem: {
      name: "",
      situation: "",
      grade: "",
    },
    defaultItem: {
      name: "",
      situation: "",
      grade: "",
    },
  }),

  computed: {
    formTitle() {
      return this.editedIndex === -1 ? "Novo Aluno" : "Editar Aluno";
    },
  },

  watch: {
    dialog(val) {
      val || this.close();
    },
    dialogDelete(val) {
      val || this.closeDelete();
    },
  },

  created() {
    this.initialize();
  },

  methods: {
    initialize() {
      this.tests = [
        {
          id: 0,
          name: "Algoritmo",
          situation: "Aprovado",
          grade: 7.0,
        },
        {
          id: 1,
          name: "Logica matematica",
          situation: "Aprovado",
          grade: 8.0,
        },
        {
          id: 2,
          name: "Machine learning",
          situation: "Aprovado",
          grade: 9.0,
        },
      ];
    },

    editItem(item) {
      this.editedIndex = this.tests.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialog = true;
      console.log("edit Data");
    },

    deleteItem(item) {
      this.editedIndex = this.tests.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialogDelete = true;
      console.log("delete Data");
    },

    deleteItemConfirm() {
      this.tests.splice(this.editedIndex, 1);
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
        Object.assign(this.tests[this.editedIndex], this.editedItem);
      } else {
        this.tests.push(this.editedItem);
      }
      this.close();
    },
  },
};
</script>