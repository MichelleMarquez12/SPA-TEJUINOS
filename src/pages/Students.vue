<template>
    <div class="page-body flex"
        style="background-color: rgb(227,205,174); top: 10;left: 0;font-family:'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;">
        <div>
            
            <div style="margin: 1% 3%;" >
                <label style="display: flex;">Ingrese el nombre del estudiante que desea encontrar y presione ENTER: </label>
                <input class="rounded-xl px-2" type="text" name="search" id="search" placeholder="Buscar" v-model="search" @input="changeKey">
            </div>
            <div class="student-list rounded"
                style="width: 100%;min-width: 500px; margin: 0 3%; background-color: #fff; padding: 1%; box-shadow: 0px 2px 10px rgba(0, 0, 0, 0.1);overflow: scroll; max-height: 500px; height: 500px;">
                <StudentList @globalstudent="setId" :search="search" :key="componentKey"></StudentList>
            </div>
        </div>

        <div v-if="empty == true"
            style="margin-top:5%;margin-left: 5%;background-color: #fff; display: flex; top: 10; left: 0; width: 50%; height: 50%; border-radius: 5px; box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);">
            <div class="p-3" @click="sendId">
                <div v-html="url_avatar"
                    style="border-radius: 100%;border: solid 1px #808080;overflow: hidden; margin:0 auto 5px auto;width: 250px;height: 250px;" > </div>
                <div style="width: 100%;">
                    <p style="margin-bottom: 12px; font-size: large; font-weight: bold;">{{ this.student.name }} {{
                        this.student.last_name }}</p>
                    <p style="margin-bottom: 2px;font-size: small;"> {{ num_ctrl }} </p>
                    <p style="margin-bottom: 2px;font-size: small;"> {{ this.student.gender }} </p>
                    <p style="margin-bottom: 2px;font-size: small;"> {{ this.student.dob }} </p>
                    <p style="margin-bottom: 2px;font-size: small;"> {{ this.student.email }} </p>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import StudentList from '../components/StudentList.vue';

export default {
    name: "StudentsPage",
    data() {
        return {
            title: "Directorio de Estudiantes",
            url_avatar: "",
            num_ctrl: "",
            student: Object,
            empty: false,
            search: '',
            componentKey : 0
        };
    },
    methods: {
        setId(student) {
            this.student = student;
            this.empty = true;
            this.setctrlnum();
            this.makenewurl();
        },
        setctrlnum() {
            this.num_ctrl = this.student.email.split("@")[0]
        },
        makenewurl() {
            this.url_avatar = '<img src = "https://joesch.moe/api/v1/' + this.student.gender + '/' + this.num_ctrl + '" width="250px" height="250px" />';
        },
        changeKey(){
            this.componentKey += 1
        }
    },
    components: {
        StudentList,
    }
}

</script>