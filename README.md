# 地铁调查问卷 H5 页面 (Vue 2 版本)

这是一个用于收集地铁乘客满意度和反馈的移动端 H5 问卷页面，使用 Vue 2 框架开发。

## 功能特点

- 响应式设计，适配各种移动设备
- 包含多种问题类型：单选、评分、多选、开放性问题
- 表单验证确保必填项完成
- 组件化开发，代码结构清晰
- 美观的 UI 设计，提升用户体验
- 提交成功反馈

## 技术栈

- Vue 2
- CSS3 (Scoped CSS)
- 组件化设计

## 项目结构

```
src/
├── App.vue                # 主应用组件
├── main.js                # 入口文件
├── assets/                # 静态资源
└── components/            # 组件目录
    └── survey/            # 问卷相关组件
        ├── SurveyForm.vue         # 问卷表单主组件
        ├── SectionContainer.vue   # 问卷部分容器组件
        ├── RadioGroup.vue         # 单选题组件
        ├── RatingGroup.vue        # 评分题组件
        ├── CheckboxGroup.vue      # 多选题组件
        └── SuccessModal.vue       # 成功提交弹窗组件
```

## 如何运行

1. 确保已安装 Node.js
2. 克隆或下载本项目
3. 在项目目录中运行以下命令安装依赖：
   ```
   yarn install
   ```
   或
   ```
   npm install
   ```
4. 启动开发服务器：
   ```
   yarn serve
   ```
   或
   ```
   npm run serve
   ```
5. 在浏览器中访问 `http://localhost:12000`

## 问卷内容

问卷包含以下几个部分：

1. 基本信息（性别、年龄、乘坐频率）
2. 满意度评价（清洁度、准点率、指示标识、服务态度）
3. 乘车体验（需要改进的方面）
4. 建议与反馈
5. 联系方式（选填）

## 自定义

您可以通过修改以下文件来自定义问卷：

- `src/components/survey/SurveyForm.vue` - 修改问卷结构和问题
- 各组件的 `<style>` 部分 - 调整样式和主题颜色
- 数据模型和提交逻辑在 `SurveyForm.vue` 的 `<script>` 部分
