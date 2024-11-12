---
title: Symmetry - 推理网络  
description: 探索 Symmetry，一个与 Twinny VSCode 扩展集成的去中心化计算网络及其扩展功能。
---

Symmetry 是一个实验性的去中心化计算网络，允许用户共享和访问计算资源。最初与 Twinny VSCode 扩展集成，Symmetry 有潜力成为开发者、研究人员和数据科学家的强大工具。

**注意**：Symmetry 仍处于 alpha 版本，可能会出现一些问题。如遇到问题，请在 [https://github.com/twinnydotdev/symmetry](https://github.com/twinnydotdev/symmetry) 上报告。

![symmetry 结构图](../../../../assets/symmetry-architecture.png)

Symmetry 客户端采用 MIT 许可证。

[https://github.com/twinnydotdev/symmetry](https://github.com/twinnydotdev/symmetry)


## 在 Twinny VSCode 扩展中连接 Symmetry

如果网络中有可用的推理提供者，Symmetry 可以作为推理提供者与 Twinny VSCode 扩展配合使用。您可以在以下网址找到当前的提供者和可用模型：[https://twinny.dev/symmetry](https://twinny.dev/symmetry)。

1. 在 Twinny 扩展的设置中，选择您想要的模型。
2. 点击扩展中的“连接到 Symmetry”按钮。
3. 扩展将自动使用选定的模型连接到 Symmetry 网络。模型名称可以在 Twinny 扩展的设置中进行配置，请确保与 [https://twinny.dev/symmetry](https://twinny.dev/symmetry) 中列出的可用模型匹配。未来此过程将改进，允许用户从可用模型列表中选择。
4. 连接成功后，您将在扩展侧边栏看到绿色的“已连接”状态。
5. 尝试通过 Twinny 扩展发送一些请求，验证其是否按预期工作。

#### 未连接状态：
![symmetry 未连接](../../../../assets/symmetry_disconnected.png)

#### 已连接状态：
![symmetry 已连接](../../../../assets/symmetry_connected.png)

查看图标：

![symmetry provider](../../../../assets/symmetry_provider.png)

## 成为 Symmetry 提供者

随着 Symmetry 的发展，用户有机会通过成为提供者为网络贡献资源。以下是您需要了解的内容：

### 为什么考虑成为提供者？

- 为去中心化计算网络做出贡献
- 利用空闲计算资源
- 未来可能有奖励机制（视网络发展而定）
- 获取去中心化技术的经验
- 成为机器学习研究的数据收集者

### 如何成为提供者

1. **安装 Symmetry**：

   Unix 系统
   ```bash
   curl -fsSL https://www.twinny.dev/symmetry-unix.sh | sh
   ```

   Windows 系统
   ```bash
   iwr -useb https://www.twinny.dev/symmetry-windows.ps1 | iex
   ```

2. **配置您的节点**：
   在 `~/.config/symmetry/` 目录中创建 `provider.yaml` 文件，配置您的提供者设置。

3. **启动您的节点**：
   ```bash
   symmetry-cli
   ```

提供者将启动并执行一次测试调用：

```
ℹ️ INFO: 🔗 Initializing client using config file: /home/twinnydotdev/.config/symmetry/provider.yaml
ℹ️ INFO: 📁 Symmetry client initialized.
ℹ️ INFO: 🔑 Discovery key: xxx
ℹ️ INFO: 🔑 Server key: 4b4a9cc325d134dee6679e9407420023531fd7e96c563f6c5d00fd5549b77435
ℹ️ INFO: 🔗 Joining server, please wait.
ℹ️ INFO: 🔗 Connected to server.
ℹ️ INFO: ✅ Verification successful.
ℹ️ INFO: 👋 Saying hello to your provider...
ℹ️ INFO: 🚀 Sending test request to http://localhost:11434/v1/chat/completions
ℹ️ INFO: 📡 Got response, checking stream...
ℹ️ INFO: ✅ Test inference call successful!
```

### 程序化实现

```bash
npm install symmetry-core
```

```bash
const config = {
  apiHostname: "localhost",
  apiKey: "",
  apiPath: "/v1/chat/completions",
  apiPort: 11434,
  apiProtocol: "http",
  apiProvider: "ollama",
  dataCollectionEnabled: false,
  maxConnections: 10,
  modelName: "llama3.1:latest",
  name: "twinnydotdev",
  path: "/home/twinnydotdev/.config/symmetry/data",
  public: true,
  serverKey: "4b4a9cc325d134dee6679e9407420023531fd7e96c563f6c5d00fd5549b77435",
  systemMessage: "I'm a system message"
};

const provider = new SymmetryProvider(config);
```


### 提供者配置

`provider.yaml` 示例：

```yaml
apiHostname: localhost # 推理服务器的主机地址
apiKey: # 推理服务器的 API 密钥
apiPath: /v1/chat/completions # 推理接口路径
apiPort: 11434 # 推理服务器的端口
apiProtocol: http # 推理服务器的协议
apiProvider: ollama # 推理提供者名称
dataCollectionEnabled: true # 是否启用数据收集
maxConnections: 10 # 最大连接数
modelName: llama3:8b # 您提供的模型名称
name: provider  # 您的提供者名称
path: /home/richard/.config/symmetry/default # 数据存储目录
public: true # 是否公开访问您的提供者
serverKey: 4b4a9cc325d134dee6679e9407420023531fd7e96c563f6c5d00fd5549b77435 # Symmetry 服务器密钥
systemMessage: "I'm a system message" # 可选的系统消息
```

根据您的设置和偏好调整这些配置。

## 提供者注意事项

- 确保您的节点安全且已更新
- 注意通过您的节点传输的数据
- 保持稳定和可靠的连接

## 超越 VSCode：未来发展

虽然目前专注于 Twinny 扩展，但 Symmetry 的潜力不仅限于此：

- **独立使用**：计划开发一个 Node.js 包，使开发者可以在任何 Node.js 应用中利用 Symmetry 网络。
- **API 访问**：未来版本可能包括直接的 API 访问，支持与广泛应用和服务的集成。

## 常见问题 (FAQ)

1. **Q: Symmetry 仅限于 VSCode 用户吗？**  
   A: 目前与 Twinny VSCode 扩展集成，但未来计划通过 Node.js 包和直接 API 访问拓展 Symmetry 的可访问性。

2. **Q: 我可以用 Symmetry 做聊天和自动补全吗？**  
   目前，Symmetry 设计用于聊天，但未来可能会用于其他用途（例如自动补全）。

3. **Q: Symmetry 如何确保数据隐私？**  
   A: Symmetry 使用加密连接进行所有通信。在初始匹配后，客户端与提供者之间直接通信，绕过中央服务器。然而，提供者可以访问解密后的数据进行处理，因此在使用网络时请考虑数据的敏感性。

4. **Q: 我可以在自己的项目中使用 Symmetry 吗？**  
   目前，Symmetry 主要用于 Twinny VSCode 扩展，但计划推出 Node.js 包，使其可以在各种项目中广泛集成。

5. **Q: 成为提供者会有奖励吗？**  
   目前没有正式的奖励系统，但随着网络的发展，可能会引入奖励机制。目前作为提供者贡献网络，是一个支持去中心化技术并获得经验的机会。

6. **Q: 如何获取 Symmetry 开发的最新动态？**  
   A: 请关注 Symmetry 官方 GitHub 仓库和文档，获取最新更新和公告。

通过探索 Symmetry，无论是作为用户通过 Twinny 扩展，还是作为提供者，您都在参与去中心化计算技术的发展。随着 Symmetry 的演进，它旨在为开发者和研究人员提供更灵活、强大的选择。