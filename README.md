# vite+vue3 学习日记

## 1.使用NodeJS内置模块
如果在vite.config.ts中需要引入Node的内置模块,例如:path、url、__dirname等<br/>
提示找不到模块，原因node.js本身并不支持typescript,所以直接在typescript项目里使用是不行的<br/>
必须安装@types/node  `npm i @types/node --dev-save`

## 2. 别名配置
```javascript
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import path from "path"
// https://vitejs.dev/config/
export default defineConfig({
  resolve: {
    alias: {
      "@": path.resolve(__dirname, './src') // **官方文档要求必须使用绝对路径
    },
  },
  plugins: [vue()],
})
```

## 3.项目初始化后main.ts提示找不到模块xxxx.vue
原因是在ts中xxx.vue模块中并没有定义，所以需要开发者重写一下这些外部模块<br/>
解决办法：在vite-env.d.ts添加追加下面的代码(`如果没有这个文件可以新建一个xx.d.ts的声明文件`)
```javascript
declare module '*.vue' {
  import type { DefineComponent } from 'vue';
  const vueComponent: DefineComponent<{}, {}, any>;
  export default vueComponent;
}
```





