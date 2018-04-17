<template>
  <div class="wrap"> 
      <!-- loading -->
        <div class="item"> 
          <loading v-if="loadingState" type="svg" ></loading>
        </div>
      
      <!-- content -->
      <section v-if="!loadingState">
        <ul>
          <li v-for="(item, index) in imgs">
            <img :src="item.img" alt="">
          </li>
        </ul>

         <div class="btn">
          <button @click="test">测试</button>
        </div>
      </section>
  </div>
</template>

<script>
import loading from "@/components/loading";

export default {
  name: "App",
  data() {
    return {
      imgs: null,
      loadingState: true,
      testAPI:
        "http://rap2api.taobao.org/app/mock/10576/GET//example/1523939055547"
    };
  },
  components: {
    loading
  },
  created() {
    this.ajax();
  },
  methods: {
    // 请求测试
    ajax() {
      fetch(this.testAPI).then(r => {
        r.json().then(data => {
          if (!this.imgs) {
            this.imgs = data.imgs;
          }
          this.loadingState = false;
        });
      });
    },

  test() {
    this.loadingState = true
    setTimeout(() => {
      this.loadingState = false
    }, 2000);
  }

  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
li {
  list-style: none;
}
.wrap {
  max-width: 600px;
  margin: 0 auto;
}
.wrap .item {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

section {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}

section .btn {
  flex: 1 100%;
  text-align: center;
}

section ul {
  flex: 1 100%;
  display: flex;
  flex-wrap: wrap;
}
</style>
