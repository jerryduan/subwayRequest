# CLAUDE.md

本文件为Claude Code (claude.ai/code) 在此代码库中工作时提供指导。

## 交流语言
- 在此项目中始终使用中文回答

## 开发命令

- **启动开发服务器**: `npm run serve` 或 `yarn serve` (运行在端口 12000)
- **生产环境构建**: `npm run build` 或 `yarn build`
- **代码检查**: `npm run lint` 或 `yarn lint`
- **安装依赖**: `npm install` 或 `yarn install`

## 项目架构

这是一个Vue 2移动端H5地铁调查问卷应用，具有以下结构：

### 核心组件
- **App.vue**: 主应用包装器，包含全局样式和弹窗管理
- **SurveyForm.vue**: 主表单组件，包含所有调查逻辑和数据模型
- **组件库**: `src/components/survey/`中的可复用调查组件：
  - `SectionContainer.vue`: 表单区域包装器
  - `RadioGroup.vue`: 单选题组件
  - `RatingGroup.vue`: 5分满意度评分题组件
  - `CheckboxGroup.vue`: 多选题组件
  - `SuccessModal.vue`: 表单提交成功确认弹窗

### 数据模型
调查表单在`SurveyForm.vue`中使用集中式数据模型：
- 基本信息: 性别、年龄、频率 (均为必填)
- 满意度评分: 清洁度、准点率、标识、服务 (均为必填)
- 改进建议: 多选数组，带条件显示的"其他"文本框
- 开放反馈: 建议文本域
- 可选联系方式: 手机号码

### 关键模式
- 组件通信通过props向下传递，事件向上传递 (`$emit`)
- 通过计算属性`isFormValid`进行表单验证
- "其他"文本框的条件渲染
- 移动优先的响应式设计和作用域CSS
- 配色方案: 主要蓝色 (#0078d7)，中性灰色

### 配置
- 开发服务器运行在端口12000，启用了CORS
- ESLint使用Vue基础规则和Babel解析器
- 当前未配置测试框架