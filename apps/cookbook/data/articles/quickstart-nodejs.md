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

## 步骤2：设置您的API密钥
既然Curl正在运行，下一步是在终端或命令行中设置您的API密钥。您可以选择跳过此步骤，只需按照第3步中所述将API密钥包含在您的请求中。

要设置API密钥，您可以使用以下命令在终端或命令行中：
```
export OPENAI_API_KEY=YOUR_API_KEY
```
确保将"YOUR_API_KEY"替换为您的实际API密钥。

一旦将API密钥设置为环境变量，您可以在后续Curl请求中使用它，而无需在每个请求中手动指定API密钥。这使得使用API变得更加方便和安全。

请务必保护您的API密钥，不要将其泄露给未经授权的人。

### a.对于MacOS，以下是如何在终端中设置API密钥的步骤：

- 打开终端：您可以在"应用程序"文件夹中找到终端，或使用Spotlight（Command + Space）进行搜索。

- 编辑bash配置文件：使用以下命令打开配置文件，nano ~/.bash_profile，或者对于较新的MacOS版本，可以使用nano ~/.zshrc：
    ```
    nano ~/.bash_profile
    ```
    或
    ```
    nano ~/.zshrc
    ```

- 添加环境变量：在编辑器中，添加以下行，将"your-api-key-here"替换为您的实际API密钥：
    ```
    export OPENAI_API_KEY='your-api-key-here'
    ```
- 保存并退出：按Ctrl+O保存更改，然后按Ctrl+X关闭编辑器。

- 加载配置文件：使用以下命令加载已更新的配置文件：

    ```
    source ~/.bash_profile
    ```

    或

    ```
    source ~/.zshrc
    ```

- 验证设置：在终端中键入以下命令来验证设置，它应该显示您的API密钥：
    ```
    echo $OPENAI_API_KEY
    ```

这将显示您的API密钥，表示您已成功设置了环境变量。确保保护好您的API密钥，不要将其泄露给未经授权的人。

### b. 对于Windows，以下是如何在命令提示符中设置API密钥的步骤：


- 打开命令提示符：您可以通过在开始菜单中搜索"cmd"来找到它。
    
- 在当前会话中设置环境变量：要在当前会话中设置环境变量，请使用以下命令，将"your-api-key-here"替换为您的实际API密钥：
    ```
    setx OPENAI_API_KEY "your-api-key-here"
    ```
    此命令将为当前会话设置OPENAI_API_KEY环境变量。

- 永久设置：要使设置永久生效，可以通过系统属性进行如下设置：

    - 右键单击"This PC"或"My Computer"，然后选择"属性"。

    - 单击"高级系统设置"。

    - 单击"环境变量"按钮。

    - 在"系统变量"部分，单击"新建..."，然后输入OPENAI_API_KEY作为变量名，将您的API密钥输入为变量值。

- 验证设置：要验证设置，请重新打开命令提示符，然后键入以下命令。它应该显示您的API密钥：


```echo %OPENAI_API_KEY%```

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