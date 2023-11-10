---
pub-date: 2023-11-10
author: Jay
---

# 开发者快速入门 Python
Node.js是一种流行的JavaScript框架，通常用于Web开发。OpenAI提供了一个自定义的Node.js/TypeScript库，使在JavaScript中使用OpenAI API变得简单而高效。


## 步骤1：设置Node
### 安装Node.js
要使用OpenAI Node.js库，您需要确保已安装Node.js。

要下载Node.js，请前往官方Node网站，并下载LTS版本。如果您是首次安装Node.js，可以按照官方Node.js使用指南开始使用。

### 安装OpenAI Node.js库
一旦您安装了Node.js，就可以安装OpenAI Node.js库。从终端/命令行中运行以下命令：

```
npm install openai
```

或者，如果您使用Yarn包管理器，可以运行：
```
yarn add openai
```

这将安装OpenAI Node.js库，使您能够在Node.js应用程序中使用OpenAI API。

## 设置API密钥供所有项目使用（推荐）
将API密钥设置为所有项目可访问的主要优势是，Python库将自动检测并使用它，无需编写任何代码。

要设置API密钥，您可以将其添加到您的环境变量中，或者您可以在代码中直接指定API密钥。以下是如何将API密钥添加到环境变量中的示例：

打开终端/命令行。

在终端/命令行中，运行以下命令，将您的OpenAI API密钥添加为环境变量，将"YOUR_API_KEY"替换为您的实际API密钥：

在Unix或MacOS上：


```
export OPENAI_API_KEY=YOUR_API_KEY
```

在Windows上：


```
set OPENAI_API_KEY=YOUR_API_KEY
```
确保将实际的API密钥替换为"YOUR_API_KEY"。

一旦将API密钥添加到环境变量中，您可以在任何项目中使用OpenAI Python库，而无需在每个项目中手动指定API密钥。库将自动从环境变量中读取API密钥。

请确保保护您的API密钥，不要将其泄露给未经授权的人。



## 步骤3：发送您的第一个API请求
## 发出API请求
在配置了Node.js并设置了API密钥后，最后一步是使用Node.js库向OpenAI API发送请求。为此，请使用终端或集成开发环境（IDE）创建一个名为openai-test.js的文件。

在文件中，复制并粘贴以下示例之一：
```
import OpenAI from "openai";

const openai = new OpenAI();

async function main() {
  const completion = await openai.chat.completions.create({
    messages: [{ role: "system", content: "You are a helpful assistant." }],
    model: "gpt-3.5-turbo",
  });

  console.log(completion.choices[0]);
}

main();
```
要运行代码，请在终端/命令行中输入以下命令：node openai-test.js。

聊天补全示例突显了我们的模型的一个优势领域：创造性能力。用形式良好的诗歌解释递归（编程主题）是最优秀的开发者和最优秀的诗人都会感到困难的任务。在这种情况下，gpt-3.5-turbo毫不费力地完成了这个任务。这展示了OpenAI模型的强大文本生成能力。


对于聊天补全API的示例：

```
const { OpenAIApi, CreateCompletionRequest } = require("openai");

const openai = new OpenAIApi({ key: "your-api-key-here" });

const request = new CreateCompletionRequest({
  engine: "text-davinci-002",
  prompt: "Translate the following English text to French: \"$text\"",
  max_tokens: 60,
});

openai.createCompletion(request)
  .then(response => {
    console.log(response.choices[0].text);
  })
  .catch(error => {
    console.error(error);
  });
```

对于嵌入API的示例：
```
const { OpenAIApi, CreateEmbeddingRequest } = require("openai");

const openai = new OpenAIApi({ key: "your-api-key-here" });

const request = new CreateEmbeddingRequest({
  engine: "davinci-codex",
  documents: ["An apple"],
});

openai.createEmbedding(request)
  .then(response => {
    console.log(response);
  })
  .catch(error => {
    console.error(error);
  });
```

请确保将"your-api-key-here"替换为您的实际API密钥。然后，运行这个Node.js文件，它将使用OpenAI API执行您的请求并返回结果。

## 下一步
既然您已经发出了您的第一个OpenAI API请求，现在是时候探索更多可能性了：

- 要了解有关我们的模型和API的详细信息，请参阅我们的[GPT指南](https://platform.openai.com/docs/guides/gpt)。
- 访问[OpenAI Cookbook](https://cookbook.openai.com/)，了解深入的示例API用例以及常见任务的代码片段
- 想知道OpenAI的模型能做什么？查看我们的示例[提示库](https://platform.openai.com/examples)。
- 想尝试API而不写任何代码吗？开始在[Playground](https://platform.openai.com/playground)中进行实验。
- 在开始构建项目时，请牢记我们的[使用政策](https://openai.com/policies/usage-policies)。
- 继续探索和实验，以充分利用OpenAI API的强大功能。祝您成功！