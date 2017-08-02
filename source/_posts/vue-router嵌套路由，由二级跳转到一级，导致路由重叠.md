---
title: vue-router嵌套路由跳转重叠问题
date: 2017-03-02 22:32:22
tags: 
- js
- vue
categories: 
- frame
- vue
---

#### 现在有/1、/2、/3两个一级路由，/1下面有/1/a子路由（二级路由），当从/1/a上跳至/2是，**偶尔**会出现跳到/1/2上面,而且此时在切换1,2,3时，会变成/1/1,/1/2,/1/3，来回切换时会**突然**变正常。

- router/index.js(路由设置)

  ```javascript
  const router = new Router({
    routes: [
      { path: '/', redirect: '/apply' },
      { path: '/apply', name: 'apply', component: Apply },
      { path: '/myauth', name: 'myauth', component: MyAuth },
      { path: '/approval', name: 'approval', component: Approval },
      { path: '/manage', component: Manage,
        children: [
          { path: '', component: ManageIndex },
          { path: 'RoleMenu', name: 'RoleMenu', component: RoleMenu },
          { path: 'RoleMember', name: 'RoleMember', component: RoleMember }
        ]
      }
    ],
    mode: 'history'
  })
  ```

- app.vue(一级路由侧栏)

  ```html
  <el-row>
        <el-col :xs="24" :sm="4" :md="3" :lg="2">
          <el-menu router class="list" :default-active="active">
            <el-menu-item index="apply">
              <router-link to="/apply" class="router-item" >权限申请</router-link>
            </el-menu-item>
            <el-menu-item index="myauth" @click.native="getAuthData">
              <router-link to="/myauth" class="router-item">
                <span>我的权限</span>
                <span class="my-badge" v-show="newAuthNum > 0">{{newAuthNum}}</span>
              </router-link>
            </el-menu-item>
            <el-menu-item index="approval">
              <router-link to="/approval" class="router-item">
                <span>我的审批</span>
                <span class="my-badge" v-show="approvalNum > 0">{{approvalNum}}</span>
              </router-link>
            </el-menu-item>
            <el-menu-item index="manage">
              <router-link to="/manage" class="router-item">权限管理</router-link>
            </el-menu-item>
          </el-menu>
        </el-col>
        <el-col :xs="24" :sm="20" :md="21" :lg="22">
          <keep-alive>
            <router-view :new-msg="newMsg" :user-msg="userMsg" ref="myauth"></router-view>
          </keep-alive>
        </el-col>
      </el-row>
  ```

- ManageIndex.vue(一级路由进入二级路由)

  ```javascript
  roleMenu (index, rows) {
      this.$router.push({name: 'RoleMenu', query: {id: rows[index].id, role: encodeURIComponent(rows[index].role)}})
  },
  ```

- RoleMenu.vue(二级路由返回一级路由)

  ```javascript
  <el-button type="text"><router-link to="/Manage"><i class="el-icon-arrow-left"></i></router-link></el-button>
  ```

#### 解决

- 尝试过的解决办法：

  ```javascript
  1.使用this.$router.push跳转侧栏
  2.配置子路由的path为'/RoleMenu'，这样就是同一级目录，跳转到的是'.com/RoleMenu'而不是'.com/manage/RoleMenu'，虽然可以正常显示，但因为需求原因无法采取这种解决办法
  ```

- 其实是element-ui的问题，只需要index属性当作路由名称就可以了，不需要使用router-link这个指令了,我这里还用了个点击事件来切换路由，其实没必要的了

  ```html
  <Navmenu mode="vertical" :router="true" :unique-opened="isMobile" default-active="1" menu-trigger="click">
              //这里index就是路由path了
              <Navmenuitem index="index" @click="menuItemClick('AdminHome')">
                  <i class="icon-desktop"></i>主页
              </Navmenuitem>
              <Navsubmenu index="2">
                  <div slot="title"><i class="icon-file-alt"></i>文章</div>
                  <Navmenuitemgroup>
                      <Navmenuitem index="article" @click="menuItemClick('AdminArticle')">
                          <i class="icon-list-alt"></i>文章列表
                      </Navmenuitem>
                      <Navmenuitem index="addArticle" @click="menuItemClick('AdminAddArticle')">
                          <i class="icon-plus-sign-alt"></i>添加文章
                      </Navmenuitem>
                      <Navmenuitem index="adminComment" @click="menuItemClick('AdminArticleComment')">
                          <i class="icon-comments"></i>文章评论
                      </Navmenuitem>
                  </Navmenuitemgroup>
              </Navsubmenu>
              <Navsubmenu index="3">
                  <div slot="title"><i class="icon-plus-sign-alt"></i>标签归类</div>
                  <Navmenuitemgroup>
                      <Navmenuitem index="adminTag" @click="menuItemClick('AdminTag')">
                          <i class="icon-tags"></i>标签列表
                      </Navmenuitem>
                      <Navmenuitem index="adminCategory" @click="menuItemClick('AdminCategory')">
                          <i class="icon-paste"></i>分类列表
                      </Navmenuitem>
                  </Navmenuitemgroup>
              </Navsubmenu>
              <Navmenuitem index="adminMessage" @click="menuItemClick('AdminMessage')">留言列表</Navmenuitem>
              <Navmenuitem index="adminCount" @click="menuItemClick('AdminCount')">访问记录</Navmenuitem>
          </Navmenu>
  ```

- 其他思路

  ```json
  {
        path: '/server',
        name: 'server',
        component: server,
        children: [
          {
            path: '/server/server_index',
            component: serverIndex
          },
          {
            path: '/server/settlement',
            component: settlement
          },
          {
            path: '/server/server_ratings',
            component: serverRatings
          }
        ]
      },
  ```

  ​