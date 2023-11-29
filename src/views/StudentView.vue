<template>
  <div>
    <div class="card">
      <div class="card-header">
        <h4>Students</h4>
        <button type="button" class="btn btn-primary float-end" data-bs-toggle="modal" data-bs-target="#exampleModal">
          Add Student
        </button>
      </div>
      <div class="card-body">
        <table class="table table-bordered">
          <thead>
            <tr>
              <th>Id</th>
              <th>Name</th>
              <th>Age</th>
              <th>Salary</th>
              <th>Phone</th>
            </tr>
          </thead>
          <tbody v-if="this.students.length > 0">
            <tr v-for="(student, index) in students" :key="index">
              <td>{{ student.id }}</td> 
              <td>{{ student.name }}</td>
              <td>{{ student.age }}</td>
              <td>{{ student.salary }}</td>
              <td>{{ student.phone }}</td>
            </tr>
          </tbody>
          <tbody v-else>
            <tr>
              <td colspan="5"><p style="text-align: center;">Loading....</p></td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
  <!-- Modal -->
<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h1 class="modal-title fs-5" id="exampleModalLabel">Add student</h1>
            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
          </div>
          <div class="modal-body">
            <form @submit.prevent="addStudent">
              <p v-if="errors.length">
              <b>Please correct the following error(s):</b>
              <ul>
                <li v-for="error in errors">{{ error }}</li>
              </ul>
            </p>
              <div class="mb-3">
                <label for="inputName" class="form-label">Name</label>
                <input v-model="newStudent.name" type="text" class="form-control" id="inputName">
              </div>
              <div class="mb-3">
                <label for="inputSalary" class="form-label">Salary</label>
                <input v-model="newStudent.salary" type="number" class="form-control" id="inputSalary">
              </div>
              <div class="mb-3">
                <label for="inputAge" class="form-label">Age</label>
                <input v-model="newStudent.age" type="number" class="form-control" id="inputAge">
              </div>

              <div class="mb-3">
                <label for="inputPhone" class="form-label">Phone</label>
                <input v-model="newStudent.phone" type="number" class="form-control" id="inputPhone">
              </div>
              <button  type="submit" class="btn btn-primary float-end">Create Student</button>
            </form>
          </div>
        </div>
      </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'students',
  data() {
    return {
      students: [],
      newStudent: {
        name: '',
        salary: '',
        age: '',
        phone: '',
      },
      errors: [], 
    };
  },

  mounted() {
    this.getStudents();
  },

  methods: {
    getStudents() {
      axios.get('http://vue-api.test/api/get-student').then((res) => {
        this.students = res.data.data;
        console.log('Students:', this.students);
      });
    },

    addStudent() {
      // Basic form validation
      this.errors = [];

      if (!this.newStudent.name.trim()) {
        this.errors.push('Name is required.');
      }

      if (!this.newStudent.salary) {
        this.errors.push('Salary is required.');
      }

      if (!this.newStudent.age) {
        this.errors.push('Age is required.');
      }

      if (!this.newStudent.phone) {
        this.errors.push('Phone is required.');
      }

      // If there are validation errors, prevent form submission
      if (this.errors.length > 0) {
        return;
      }

      // If no errors, proceed with adding the student
      axios.post('http://vue-api.test/api/create-student', this.newStudent)
        .then((res) => {
          console.log('New Student:', res.data);
          this.newStudent = {
            name: '',
            phone: '',
            salary: '',
            age: '',
          };
          this.getStudents();
        })
        .catch((error) => {
          console.error('Error adding student:', error);
        });
    },
    closeModal() {
      const modal = new bootstrap.Modal(document.getElementById('exampleModal'));
      modal.hide();
    },
  }
}
</script>
