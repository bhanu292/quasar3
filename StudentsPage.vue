<template>
    <q-page class="q-pa-md">
        <h5>Student Management</h5>
        <q-card>
            <q-card-section>
                <q-input
                  v-model="newStudent"
                  label="Student Name"
                  filled />

                  <div class="q-mt-md">
                    <q-btn
                    label="Add Student"
                    icon="Person_add"
                    color="positive"
                    class="q-mr-sm"
                    @click="addStudent"/>

                    <q-btn
                    label="Remove Last"
                    icon="delete"
                    color="negative"
                    @click="removeStudent"/>
                  </div>
            </q-card-section>
        </q-card>

        <q-seperator class="q-my-md" />

        <!--Total-->
        <div class="text-subtitle1">
            Total Students:
            <q-badge :color="badgeColor">{{ totalStudents }}</q-badge>
        </div>

        <!--Empty-->
        <p v-if="students.length === 0" class="text-grey q-mt-md">
            No students found
        </p>

        <!--Student List-->
        <q-list bordered v-else>

            <q-item v-for="(student, index) in students" :key="index">
            <q-item-section>

                <!--View Mode-->
                <div v-if="!student.isEditing">
                    {{ student.name }}
                </div>

                <!--Edit Mode-->
                <q-input
                v-else
                v-model="student.name"
                dense
                autofocus/>
            </q-item-section>

            <!--Actions-->
            <q-item-section side>
                <q-btn
                v-if="!student.isEditing"
                icon="edit"
                flat
                color="primary"
                @click="editStudent(index)"/>

                <q-btn
                v-if="student.isEditing"
                icon="check"
                flat
                color="positive"
                @click="mdiContentSaveEdit(index)"/>

                <q-btn 
                icon="delete"
                flat
                color="negative"
                @click="deleteStudent(index)"/>
            </q-item-section>
            </q-item>

            </q-list>

    </q-page>
    </template>

    <script>
        export default {
            name: 'StudentPage',

            data () {
                return {
                    newStudent: '',
                    students: []
                }
            },

            computed: {
                totalStudents () {
                    return this.students.length
                },

                badgeColor () {
                    return this.totalStudents === 0 ? 'grey' : 'primary'
                }
            },

            mounted () {
                const saved = localStorage.getItem('students')
                if(saved) {
                    this.students = JSON.parse(saved)
                }
            },

            methods: {
                saveToLocalStorage () {
                    localStorage.setItem('students',JSON.stringify(this.students))
                },
                addStudent () {
                    if (this.newStudent !== '') {
                        this.students.push({
                            name: this.newStudent,
                        isEditing: false
                    })
                        this.newStudent = ''
                        this.saveToLocalStorage()
                    }
                },

                editStudent (index) {
                    this.students[index].isEditing = true
                },

                savedEdit (index) {
                    this.students[index].isEditing = false
                    this.saveToLocalStorage()
                },

                deleteStudent (index) {
                        this.students.splice(index, 1)
                        this.saveToLocalStorage()
                    }
                }
        }
    </script>