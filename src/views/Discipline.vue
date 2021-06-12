<template>
  <div class="discipline pa-6">
    <v-container>
      <v-row>
        <v-list-item>
          <v-col cols="12" md="4">
            <v-text-field
              v-model="newDisciplineName"
              :counter="25"
              label="Nome da materia"
              required
              clearable
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="4">
            <v-text-field
              v-model="newDisciplineAbout"
              :counter="50"
              label="Sobre"
              required
              clearable
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="4">
            <v-text-field
              v-model="newDisciplineTeacher"
              :counter="25"
              label="Professor"
              required
              clearable
            ></v-text-field>
          </v-col>
        </v-list-item>
      </v-row>

      <!-- Materias -->
      <v-btn text class="ma-2" elevation="2" @click="addDiscipline">
        Cadastrar
      </v-btn>
    </v-container>

    <v-expansion-panels>
      <v-expansion-panel v-for="discipline in disciplines" :key="discipline.id">
        <v-expansion-panel-header>
          {{ discipline.name }}
        </v-expansion-panel-header>
        <v-expansion-panel-content>
          Sobre: {{ discipline.about }}
          <v-divider></v-divider>
          Professor: {{ discipline.teacher }}
        </v-expansion-panel-content>
      </v-expansion-panel>
    </v-expansion-panels>
  </div>
</template>

<script>
export default {
  name: "Discipline",
  data() {
    return {
      newDisciplineName: "",
      newDisciplineAbout: "",
      newDisciplineTeacher: "",

      disciplines: [
        {
          id: 1,
          name: "Algoritimo",
          about: "Introdução à Programação",
          teacher: "Wesley",
        },
        {
          id: 2,
          name: "Logica matematica",
          about:
            "Sub-área da matemática que explora as aplicações da lógica formal para a matemática",
          teacher: "Adalberto",
        },
        {
          id: 3,
          name: "Machine learning",
          about:
            "Ramo da inteligência artificial baseado na ideia de que sistemas podem aprender com dados, identificar padrões e tomar decisões com o mínimo de intervenção humana.",
          teacher: "Daniele",
        },
        {
          id: 4,
          name: "Data Science",
          about:
            "Estudo e a análise de dados econômicos, financeiros e sociais, estruturados e não-estruturados, que visa a extração de conhecimento, detecção de padrões e/ou obtenção de insights para possíveis tomadas de decisão.",
          teacher: "Vilson",
        },
      ],
    };
  },
  methods: {
    addDiscipline() {
      let newDiscipline = {
        id: Date.now(),
        name: this.newDisciplineName,
        about: this.newDisciplineAbout,
        teacher: this.newDisciplineTeacher,
      };
      this.disciplines.push(newDiscipline);
      (this.newDisciplineName = ""), (this.newDisciplineAbout = "");
      this.newDisciplineTeacher = "";
    },
  },
};
</script>

