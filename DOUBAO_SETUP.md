# 豆包 Seedream 4.0 图像生成模型集成说明

## 🎯 功能概述

本项目现已支持火山引擎豆包的 `doubao-seedream-4.0` 图像生成模型，与现有的 DALL-E-2 和 DALL-E-3 模型形成完整的图像生成解决方案。

## 🔧 配置方法

### 1. 修改配置文件

在 `config.json` 中设置：

```json
{
  "text_to_image": "doubao-seedream-4.0",
  "open_ai_api_base": "https://ark.cn-beijing.volces.com/api/v3",
  "open_ai_api_key": "YOUR_VOLCANO_API_KEY",
  "image_create_prefix": ["画"],
  "image_create_size": "1024x1024",
  "doubao_image_quality": "standard"
}
```

```json
{
  "text_to_image": "doubao-seedream-4-0-250828",
  "open_ai_api_base": "https://ark.cn-beijing.volces.com/api/v3",
  "open_ai_api_key": "YOUR_VOLCANO_API_KEY",
  "image_create_prefix": ["画"],
  "image_create_size": "1024x1024",
  "doubao_watermark": true
}
```

### 2. 支持的配置项

- `text_to_image`: 设置为 `"doubao-seedream-4-0-250828"` 启用豆包图像生成
- `image_create_size`: 图像尺寸，支持 `"1024x1024"`, `"512x512"`, `"2K"` 等
- `doubao_watermark`: 是否添加水印，默认 `true`
- `open_ai_api_base`: 火山引擎 API 基础 URL
- `open_ai_api_key`: 火山引擎 API 密钥

## 📝 使用方法

在聊天界面中，以 "画" 开头的消息会触发图像生成：

```
画一个美丽的风景
画一只可爱的小猫
画一幅抽象艺术作品
```

## 🔄 支持的模型

现在项目支持以下图像生成模型：

1. **DALL-E-2** (`dall-e-2`) - OpenAI 经典图像生成模型
2. **DALL-E-3** (`dall-e-3`) - OpenAI 最新图像生成模型  
3. **豆包 Seedream 4.0** (`doubao-seedream-4-0-250828`) - 火山引擎图像生成模型

## 🛠️ 技术实现

### 代码结构

1. **常量定义** (`common/const.py`)
   - 添加了 `DOUBAO_SEEDREAM_4_0` 常量

2. **主要实现** (`bot/chatgpt/chat_gpt_bot.py`)
   - `create_img_doubao()` - 豆包图像生成主方法
   - `create_img()` - 统一的图像生成路由方法
   - 支持重试机制和错误处理

3. **API 调用流程**
   ```
   用户请求 → create_img() → create_img_doubao() → 火山引擎 API → 返回图像 URL
   ```

## 🚀 特性优势

- **多模型支持**: 可以根据需要灵活切换不同的图像生成模型
- **统一接口**: 所有图像生成模型使用相同的调用方式
- **错误处理**: 完善的错误处理和重试机制
- **配置灵活**: 支持多种图像尺寸和质量设置

## 📋 注意事项

1. 需要有效的火山引擎 API 密钥
2. 确保网络可以访问火山引擎 API 服务
3. 图像生成可能需要一定时间，请耐心等待
4. 建议根据实际需求调整图像质量和尺寸设置

## 🔍 调试信息

日志中会显示以下信息：
- `[DOUBAO] 图像生成请求: {prompt}` - 请求开始
- `[DOUBAO] 图像生成成功: {url}` - 生成成功
- `[DOUBAO] 图像生成失败: {error}` - 生成失败

## 🆕 更新记录

- **v1.0** - 初始集成豆包 Seedream 4.0 模型
- 支持基础图像生成功能
- 添加完善的错误处理和重试机制