# Vue

## vue router

### 建立 router 資料夾

### 建立 index.js

//index.js

```
import { createRouter, createWebHistory } from 'vue-router';
import WelcomePage from '../views/WelcomePage.vue';
import HomePage from '../views/HomePage.vue';

const routes = [
    { path: '/', name: 'WelcomePage', component: WelcomePage },
    { path: '/home', name: 'homePage', component: HomePage },
];
const router = createRouter({
    history: createWebHistory(),
    routes,
});

export default router;

```

### 在`main.js`中加入

```
import router from './router/index.js';
// console.log(router)

createApp(App).mount('#app');
||加上use(router)
createApp(App).use(router).mount('#app');
```

### 在`app.vue`中加入

```
<router-view></router-view>
```

### 使用`<router-link>`替換`a`標籤

```
<a href="" class="enterButton">ENTER</a>
=>
<router-link to="/home" class="enterButton">ENTER</router-link>
<router-link :to="{ name: 'homePage' }" class="enterButton">ENTER</router-link>
```
