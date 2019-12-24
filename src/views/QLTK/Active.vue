<template>
  <div class>
    <header-active>
      <p>Tài khoản đang hoạt động.</p>
    </header-active>
    <content-active></content-active>
    <show-list-active :HeaderTable="HeaderTable"></show-list-active>
    <ul v-if="posts && posts.length">
      <li v-for="post of posts" :key="post">
        <p>
          <strong>{{post.title}}</strong>
        </p>
        <p>{{post.body}}</p>
      </li>
    </ul>

    <ul v-if="errors && errors.length">
      <li v-for="error of errors" :key="error">{{error.message}}</li>
    </ul>
  </div>
</template>
<script>
import axios from "axios";
import HeaderActive from "./components/HeaderActive";
import ContentActive from "./components/ContentActive";
import ShowListActive from "./components/ShowListActive";

export default {
  components: {
    HeaderActive,
    ContentActive,
    ShowListActive
  },
  props: {
    source: String
  },
  data: () => ({
    drawer: null,
    HeaderTable: [
      { name: "Tên Tài Khoản" },
      { name: "Họ Và Tên" },
      { name: "Giới Tính" },
      { name: "Email" },
      { name: "Số Điện Thoại" },
      { name: "Quyền" },
      { name: "Trạng Thái" },
      { name: "" }
    ],
    posts: [],
    errors: []
  }),
  created() {
    axios.get(`https://admin-htactive.herokuapp.com/api/cv-apply/5de24c1a98347824183d9313`)
    .then(response => {
      this.posts = response.data
    })
    .catch(e => {
      this.errors.push(e)
    })
  }
};
</script> 