<template>
  <div class="flex" style="border-radius: 1rem; margin-bottom: 2%; padding: 5%; box-shadow: 2px 2px 5px gray;"
    @click="sendId">
    <div v-html="url_avatar" style="border-radius: 100%;border: solid 1px #808080; margin-right: 2%;overflow: hidden;">
    </div>
    <div>
      <p style="font-size: large;"> {{ student.name }} {{ student.last_name }}</p>
      <p style="color: #404040;"> {{ num_ctrl }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'StudentItem',
  props: {
    student: {
      type: Object,
      required: true,
    }
  },
  data() {
    return {
      url_avatar: "",
      num_ctrl: ""
    }
  },
  methods: {
    setid() {
      this.num_ctrl = this.student.email.split("@")[0]
    },
    makenewurl() {
      this.url_avatar = '<img src = "https://joesch.moe/api/v1/' + this.student.gender + '/' + this.num_ctrl + '" width="100px" height="100px" />';
    },
    sendId() {
      this.$emit("send-student", this.student)
    }
  },
  mounted() {
    this.setid(),
      this.makenewurl()
  }
};
</script>