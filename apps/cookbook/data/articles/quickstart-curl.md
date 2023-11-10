---
pub-date: 2023-11-10
author: Jay
---

# 开发者快速入门 Curl
Curl是一种流行的命令行工具，由开发者用于向API发送HTTP请求。它需要较少的设置时间，但比像Python或JavaScript这样的完整特性编程语言功能有限。


## 安装Curl
许多操作系统默认情况下都提供Curl。您可以通过打开终端或命令行，然后输入以下命令来检查是否已安装Curl：

```
curl https://platform.openai.com
```
如果Curl已设置并且您已连接到互联网，它将发送一个HTTP请求以获取"platform.openai.com"的内容。

如果您收到Curl未找到的错误消息，您可以按照[Curl主页](https://everything.curl.dev/get)上的说明进行安装。

### 步骤2：设置您的API密钥
既然Curl正在运行，下一步是在终端或命令行中设置您的API密钥。您可以选择跳过此步骤，只需按照第3步中所述将API密钥包含在您的请求中。

要设置API密钥，您可以使用以下命令在终端或命令行中：
```
export OPENAI_API_KEY=YOUR_API_KEY
```
确保将"YOUR_API_KEY"替换为您的实际API密钥。

一旦将API密钥设置为环境变量，您可以在后续Curl请求中使用它，而无需在每个请求中手动指定API密钥。这使得使用API变得更加方便和安全。

请务必保护您的API密钥，不要将其泄露给未经授权的人。



#### 对于MacOS，以下是如何在终端中设置API密钥的步骤：

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

#### 对于Windows，以下是如何在命令提示符中设置API密钥的步骤：


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

### 步骤3：发送您的第一个API请求
#### 发出API请求
一旦您设置了API密钥，最后一步就是发送您的第一个API请求。为此，下面包含了一些示例请求，涵盖了Chat Completions、Embeddings和Images API。由于在第2步中已设置了API密钥，它应该会自动通过$OPENAI_API_KEY在您的终端或命令行中引用。您也可以手动将$OPENAI_API_KEY替换为您的API密钥，但请确保如果命令包含您的API密钥，请将curl命令保持私密。

以下是发送API请求的示例：
```
curl https://api.openai.com/v1/chat/completions   -H "Content-Type: application/json"   -H "Authorization: Bearer $OPENAI_API_KEY"   -d '{
    "model": "gpt-3.5-turbo",
    "messages": [
      {
        "role": "system",
        "content": "You are a poetic assistant, skilled in explaining complex programming concepts with creative flair."
      },
      {
        "role": "user",
        "content": "Compose a poem that explains the concept of recursion in programming."
      }
    ]
  }'
```

Chat Completions API（聊天补全API）示例：
```
curl -X POST "https://api.openai.com/v1/chat/completions" -H "Authorization: Bearer $OPENAI_API_KEY" -H "Content-Type: application/json" -d '{
  "model": "gpt-4.0-turbo",
  "messages": [
    {"role": "system", "content": "You are a helpful assistant."},
    {"role": "user", "content": "Who won the world series in 2020?"},
    {"role": "assistant", "content": "The Los Angeles Dodgers won the World Series in 2020."},
    {"role": "user", "content": "Where was it played?"}
  ]
}'
```

Embeddings API（嵌入API）示例：

```
curl -X POST "https://api.openai.com/v1/engines/davinci-codex/completions" -H "Authorization: Bearer $OPENAI_API_KEY" -H "Content-Type: application/json" -d '{
  "prompt": "Translate the following English text to French: \"$text\"",
  "max_tokens": 60
}'
```

Images API（图像API）示例：
```
curl -X POST "https://api.openai.com/v1/images/generate" -H "Authorization: Bearer $OPENAI_API_KEY" -H "Content-Type: application/json" -d '{
  "model": "text-davinci-002",
  "data": "An apple"
}'
```

以上示例演示了如何使用Curl发送不同类型的API请求。确保替换相应的参数和内容以满足您的需求。请注意，API密钥是敏感信息，不要在不安全的地方共享或公开。


## 下一步
既然您已经发出了您的第一个OpenAI API请求，现在是时候探索更多可能性了：

- 要了解有关我们的模型和API的详细信息，请参阅我们的[GPT指南](https://platform.openai.com/docs/guides/gpt)。
- 访问[OpenAI Cookbook](https://cookbook.openai.com/)，了解深入的示例API用例以及常见任务的代码片段
- 想知道OpenAI的模型能做什么？查看我们的示例[提示库](https://platform.openai.com/examples)。
- 想尝试API而不写任何代码吗？开始在[Playground](https://platform.openai.com/playground)中进行实验。
- 在开始构建项目时，请牢记我们的[使用政策](https://openai.com/policies/usage-policies)。
- 继续探索和实验，以充分利用OpenAI API的强大功能。祝您成功！