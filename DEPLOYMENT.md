# 地铁调查问卷 H5 页面 (Vue 2 版本) 部署指南

本文档提供了将地铁调查问卷 H5 页面 (Vue 2 版本) 部署到生产环境的步骤和最佳实践。

## 构建生产版本

在部署之前，需要先构建生产版本：

```bash
# 使用 yarn
yarn build

# 或使用 npm
npm run build
```

这将在 `dist` 目录中生成优化后的静态文件，包括 HTML、CSS 和 JavaScript 文件。

## 部署选项

### 1. 静态网站托管服务

最简单的部署方式是使用静态网站托管服务，如：

- 阿里云 OSS
- 腾讯云 COS
- 七牛云
- GitHub Pages
- Netlify
- Vercel

#### 部署步骤（以阿里云 OSS 为例）：

1. 注册/登录阿里云账号
2. 创建 OSS Bucket，并设置为"静态网站托管"模式
3. 上传 `dist` 目录中的所有文件
4. 配置自定义域名（可选）
5. 配置 HTTPS（推荐）

### 2. Web 服务器部署

如果您已有 Web 服务器，可以按照以下步骤部署：

#### Nginx 配置示例：

```nginx
server {
    listen 80;
    server_name your-domain.com;

    # 重定向到 HTTPS（推荐）
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    server_name your-domain.com;

    # SSL 配置
    ssl_certificate /path/to/cert.pem;
    ssl_certificate_key /path/to/key.pem;

    # 网站根目录
    root /path/to/subway-survey-vue2/dist;
    index index.html;

    # 缓存静态资源
    location ~* \.(css|js)$ {
        expires 7d;
        add_header Cache-Control "public, max-age=604800";
    }

    # 处理 Vue 路由
    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

### 3. Docker 部署

如果您使用 Docker，可以创建一个简单的 Dockerfile：

```dockerfile
# 构建阶段
FROM node:14 as build-stage
WORKDIR /app
COPY package*.json ./
RUN yarn install
COPY . .
RUN yarn build

# 生产阶段
FROM nginx:alpine as production-stage
COPY --from=build-stage /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

创建 `nginx.conf` 文件：

```nginx
server {
    listen 80;
    server_name localhost;

    location / {
        root /usr/share/nginx/html;
        index index.html;
        try_files $uri $uri/ /index.html;
    }
}
```

构建和运行 Docker 镜像：

```bash
docker build -t subway-survey-vue2 .
docker run -d -p 80:80 subway-survey-vue2
```

## 数据收集配置

目前，问卷表单提交后只会在控制台打印数据。在实际部署中，您需要配置后端服务来接收和存储数据。

### 添加后端 API 集成

修改 `src/components/survey/SurveyForm.vue` 中的表单提交方法：

```javascript
submitForm() {
  if (!this.isFormValid) {
    alert('请填写所有必填项')
    return
  }

  // 发送数据到后端 API
  fetch('https://your-api-endpoint.com/submit-survey', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify(this.formData),
  })
  .then(response => {
    if (!response.ok) {
      throw new Error('网络响应不正常');
    }
    return response.json();
  })
  .then(data => {
    console.log('提交成功:', data);
    this.$emit('submit-success');
    this.resetForm();
  })
  .catch(error => {
    console.error('提交错误:', error);
    alert('提交失败，请稍后再试');
  });
}
```

## 性能优化建议

1. 启用 Vue 生产模式（构建时自动启用）
2. 使用 CDN 加速静态资源
3. 启用 GZIP/Brotli 压缩
4. 设置适当的缓存策略
5. 考虑使用 Vue 的异步组件和路由懒加载（对于更大的应用）

## 安全考虑

1. 始终使用 HTTPS
2. 实施 CSRF 保护
3. 添加适当的内容安全策略 (CSP)
4. 设置合适的 CORS 策略
5. 对用户输入进行验证和清理

## 监控与分析

考虑添加以下工具来监控和分析您的 H5 页面：

1. Google Analytics 或百度统计
2. 热力图工具（如 Hotjar）
3. 错误监控（如 Sentry）

## 测试清单

在部署前，确保完成以下测试：

- 在不同移动设备上测试（iOS 和 Android）
- 在不同浏览器中测试（Safari、Chrome、Firefox 等）
- 测试表单验证
- 测试数据提交
- 测试页面加载性能