<template>
  <div>
    <el-link type="primary" @click="backHandler">返回</el-link>
    <p>仓库名称：{{ this.$route.params.row.name }}</p>
    <!-- {{ this.$route.params }} -->
    <p>仓库编号：{{ this.$route.params.row.id }}</p>
    <p>仓库附属编号：{{ this.$route.params.row.parentId }}</p>
    <p>此仓库所属总调度中心名字:{{Pname}}</p>
    <p>产品主图:</p>
    <!-- {{this.$route.params.name}} -->
    <div class="block">
      <el-image :size="120" :src="imgUrl" />
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      src: this.$route.params.row.icon,
      Pname: "",
      imgUrl: "",
      arrayUrl: [
        "https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=2931455078,2499508238&fm=26&gp=0.jpg",
        "https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=1888069095,2993167102&fm=26&gp=0.jpg",
      ],
    };
  },
  created() {
    this.randomUrl();
  },
  methods: {
    //返回上一级
    backHandler() {
      this.$router.push({ name: "product" });
    },
    randomUrl() {
      if (this.$route.params.row.name == "河津仓") {
        this.imgUrl = this.arrayUrl[0];
        // console.log(this.imgUrl);
      } else {
        this.imgUrl = this.arrayUrl[1];
      }
      let oid = this.$route.params.row.parentId;
      this.ajax({
        methods: "GET",
        url: "http://localhost:8099/category/findParent",
        data: { id: oid },
        success: (res) => {
          this.Pname = res[0].name;
          // console.log(this.Pname);
          // console.log(res[0]);
        },
      });
    },
  },
};
</script>