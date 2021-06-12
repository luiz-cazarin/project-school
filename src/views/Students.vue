<template>
  <!-- estudantes -->
  <div class="students pa-6">
    <v-container>     
      <v-row>
      <v-list-item>
        <v-col cols="12" md="4">
          <v-text-field
            v-model="newStudentName"
            :counter="50"
            label="Nome"
            required
            clearable
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="4">
          <v-text-field
            v-model="newStudentRegistration"
            :counter="10"
            label="Matricula"
            required
            clearable
          ></v-text-field>
        </v-col>
        
        </v-list-item>
      </v-row>

        <v-btn
          text
          class="ma-2"
          elevation="2"
          @click="addStudent"
        >
        Cadastrar
        </v-btn>

    </v-container>
    <!-- Lista de Alunos -->

    <v-expansion-panels>
      <v-expansion-panel v-for="student in students" :key="student.id">
        <v-expansion-panel-header>
        <v-list-item-title>
            Nome: {{ student.name }}
        </v-list-item-title>
          <v-list-item-subtitle>
              Matricula: {{ student.registration }}
          </v-list-item-subtitle>
              <v-btn
              icon
              max-width="40"
              plain
              @click="deleteStudent(student.id)"
              > 
                <v-icon color="red">mdi-delete</v-icon>
              </v-btn>
        </v-expansion-panel-header>

        <v-expansion-panel-content v-for="discipline in student.disciplines":key="discipline.id">
          Materia: {{discipline.name}}
          <v-divider></v-divider>
          Professor: {{ discipline.teacher }}
           <v-divider></v-divider>
          Nota: {{ discipline.grade}}
           
        </v-expansion-panel-content>
      </v-expansion-panel>
    </v-expansion-panels>
  
  </div>
</template>


<script>

import disciplines from './Discipline'

export default {
  name: "Students",
  data() {
    return {
      newStudentName: "",
      newStudentRegistration: "",
      disciplines: [
        {
          id: 1,
          name: "Algoritmo",
          teacher: "Wesley",
          grade: 7,
          done: false
        },
        {
          id: 2,
          name: "Logica matematica",
          teacher: "Adalberto",
          grade: 10,
          done: false
        },
        {
          id: 3,
          name: "Machine learning",
          teacher: "Daniele",
          grade: 8.9,
          done: false
        },
        {
          id: 4,
          name: "Data Science",
          teacher: "Vilson",
          grade: 9.3,
          done: false
        },
        ],
      students: [
      {},
      ],
    };
  },

  components:{
    disciplines
  },

  methods: {
    deleteStudent(id) {
      this.students = this.students.filter((student) => student.id !== id);
    },
    informationStudent(id) {
      this.students = this.students.filter(student.id === id);
    },
    addStudent(){
      let newStudent = {
        id: Date.now(),
        name: this.newStudentName,
        registration: this.newStudentRegistration,
          disciplines: this.disciplines,
      }
      this.students.push(newStudent);
      this.newStudentName = '',
      this.newStudentRegistration= ''
      console.log(this.students);
    },

  },
};
</script>
