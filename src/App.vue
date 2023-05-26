<template>
  <div id="dynamic-component-demo" class="demo">
    <button
        v-for="tab in tabs"
        v-bind:key="tab"
        v-bind:class="['tab-button', { active: currentTab === tab }]"
        v-on:click="currentTab = tab"
      >
        {{ tab }}
      </button>
      <!-- 这里只显示一个组件，组件会在 `currentTabComponent` 改变时改变，is是个属性 -->
      <component v-bind:is="currentTabComponent" class="tab"></component>

  </div>
</template>

<script>
import TabArchive from './components/tab-archive.vue'
import TabHome from './components/tab-home.vue'
import TabPosts from './components/tab-posts.vue'

export default {
  name: 'App',
  data(){
    return{
       currentTab: "Home",
          tabs: ["Home", "Posts", "Archive"]
    };
        },
        computed: {
          // 点击按钮时，currentTab的值改变，所以计算属性 currentTabComponent 运行，返回点击按钮对应的
          // 自定义组件名"tab-xxx"（自定义组件名字母全小写且必须包含一个连字符）
          currentTabComponent: function() {
            return "tab-" + this.currentTab.toLowerCase();
          }
        },
  components: {
    // 注册子组件
    TabArchive,
    TabHome,
    TabPosts,
  }
}
</script>

<style>
.tab-button {
  /* 三个按钮的样式 */
        padding: 6px 10px;
        border-top-left-radius: 3px;
        border-top-right-radius: 3px;
        border: 3px solid #ccc;
        cursor: pointer;
        background: #f0f0f0;
        margin-bottom: -1px;
        margin-right: -1px;
      }

      .tab-button:hover {
        background: #e0e0e0;
      }

      .tab-button.active {
        /* 按钮被点击 */
        background: #0886da;
      }

       .tab {
         /* 这是三个子组件的样式，但一般子组件在自己的vue文件里设置它的样式，这里竟然在父组件里设置 */
        border: 1px solid #ccc;
        padding: 10px;
        color: red;
      }
</style>
