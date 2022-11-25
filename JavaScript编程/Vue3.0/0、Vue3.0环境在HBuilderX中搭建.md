# Network: use `--host` to expose
## 1、修改 vite.config.js 配置

```
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [vue()],
  server: {             //←
	  host:'0.0.0.0'    //← 新增内容 ←
  }                     //←
})
```

## 2、 修改 package.json 文件中 scripts 节点下的脚本，如下：

```
 "scripts": {
    "dev": "vite --host 0.0.0.0",
    "build": "vite build",
    "serve": "vite preview --host 0.0.0.0"
  },
```

## 3、执行 npx vite --host 0.0.0.0 命令后，就可以通过 (http://localhost:3000/ ) 访问了