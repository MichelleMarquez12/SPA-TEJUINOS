<template>
    <div>
        <StudentItem v-for="student in return_list" :key="student" :student="student" @send-student="setGlobalId">
        </StudentItem>
    </div>
</template>

<script>
import StudentItem from './StudentItem.vue';
import students from '../students-2023.json';

var return_list = students
export default {
    props: {
        search: {
            type: String
        }
    },
    components: {
        StudentItem,
    },
    methods: {
        setGlobalId(student) {
            this.$emit("globalstudent", student)
        }
    },
    watch: {
        search: function (newval, oldval) {
            if (!(newval == "" || oldval == "")) {
                var temp = [];
                students.forEach(student => {
                    var full_name = student.name + " " + students.last_name
                    if (full_name.toLowerCase().includes(newval.toLowerCase())) {
                        temp.push(student)
                    }
                });
                return_list = temp;
            } else {
                return_list = students
            }
        }
    },
    data() {
        return {
            return_list,
        }
    }
}

</script>