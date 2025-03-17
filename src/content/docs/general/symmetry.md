---
title: Symmetry Network
description: Explore Symmetry, a distributed computing network integrated with twinny VSCode extension and beyond.
---

Symmetry is a distributed network that allows users to share and access computational resources. Initially integrated with the twinny VSCode extension, Symmetry has potential to become a powerful tool for developers, researchers, and data scientists.

The symmetry client is licensed under the Apache 2.0 license.

[https://github.com/twinnydotdev/symmetry](https://github.com/twinnydotdev/symmetry)

## OpenAI-Compatible API

Symmetry now provides an OpenAI-compatible API that allows you to interact with the network using the same API format as OpenAI. This makes it easy to integrate Symmetry with existing applications that already use the OpenAI API.  The server is 
running at `https://twinny.dev/v1` and you can interact with it using the following endpoints:

### Using the API

The Symmetry API follows the OpenAI API format, allowing you to make requests to the network using standard OpenAI client libraries or direct HTTP requests.

#### Endpoints

- **Chat Completions**: `/v1/chat/completions` - For chat-based interactions with models on the Symmetry network

#### Example Request

```javascript
// Using fetch API
const response = await fetch('https://twinny.dev/v1/chat/completions', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    model: 'model_name',
    messages: [
      { role: 'system', content: 'You are a helpful assistant.' },
      { role: 'user', content: 'Hello, how are you?' }
    ]
  })
});

// The response is streamed as Server-Sent Events (SSE)
// You can process it using standard SSE handling
```

## Becoming a Symmetry Provider

As Symmetry grows, there's an opportunity for users to contribute by becoming providers. Here's what you need to know:

### Why Consider Becoming a Provider?

- Contribute to a distributed computing network
- Utilize idle computational resources
- Potential for future incentive systems (subject to network development)
- Gain experience with peer to peer technologies
- Become the collector of data for machine learning research 

### How to Become a Provider

1. **Install Symmetry**:

Symmetry cli requires Node.js v18 or higher.

   Unix
   ```bash
   curl -fsSL https://www.twinny.dev/symmetry-unix.sh | sh
   ```

   Windows
   ```
   iwr -useb https://www.twinny.dev/symmetry-windows.ps1 | iex
   ```

1. **Configure Your Node**:
   Create a `provider.yaml` file in `~/.config/symmetry/` with your provider settings.

2. **Start Your Node**:
   ```bash
   symmetry-cli
   ```

The provider will start and make a test call to your provider.

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

### Programatically

```bash
npm install symmetry-core
```

```javascript
const config = {
  apiHostname: "localhost",
  apiKey: "apikeyforprovider", // not publically available or transported to server
  apiBasePath: "/v1",
  apiPort: 11434,
  apiProtocol: "http",
  modelName: "llama3.1:latest",
  name: "twinnydotdev",
  serverKey: "4b4a9cc325d134dee6679e9407420023531fd7e96c563f6c5d00fd5549b77435",
  systemMessage: "I'm a system message",
  userSecret: "supersecretpasswordforuptimetracking"
};

const provider = new SymmetryProvider(config);
```

### Via the Twinny Visual Studio Code Extension

The Twinny VSCode extension allows you to use your locally configure your provider to connect and share computing resources with other providers and users.

### Provider Configuration

Example `provider.yaml`:

```yaml
apiHostname: localhost # The host of your inference server
apiKey: # The API key for your inference server
apiBasePath: /v1 # The path to the inference endpoint
apiPort: 11434 # The port of your inference server
apiProtocol: http # The protocol of your inference server
modelName: llama3:8b # The name of the model you are serving
name: provider  # The name of your provider
serverKey: 4b4a9cc325d134dee6679e9407420023531fd7e96c563f6c5d00fd5549b77435 # The symmetry server key which handles provider messages
systemMessage: "Im a system message" # Optional system message for all chats
userSecret: "supersecretpasswordforrewardtracking" # A secret for uniquely identify peers on the network
```

Adjust these settings based on your setup and preferences.

## Considerations for Providers

- Ensure your node is secure and up-to-date
- Be aware of the data passing through your node
- Maintain a stable and reliable connection

#### Rate Limiting

The API includes rate limiting to ensure fair usage:
- Maximum requests per time window (configurable by the server)
- Requests exceeding the limit will receive a 429 status code with an error message

#### Conversation Management

The API supports conversation management through conversation IDs:
- Include an `id` field in your request to maintain conversation context
- The server will track messages within the same conversation

## Beyond VSCode: Future Developments

While initially focused on the twinny extension, Symmetry's capabilities now extend further:

- **OpenAI-Compatible API**: Symmetry now provides an API that follows the OpenAI format, making it easy to integrate with existing applications.
- **Standalone Usage**: A Node.js package allows developers to tap into the Symmetry network from any Node.js application.
- **WebSocket Stats**: Real-time statistics about the network are available via WebSocket connections.

## Frequently Asked Questions (FAQs)

1. **Q: Is Symmetry only for VSCode users?**
   A: While currently integrated with the twinny VSCode extension, there are plans to expand Symmetry's accessibility through a Node.js package and potentially direct API access in the future.

2. **Q: Can I use Symmetry for chat and autocomplete?**
   Currently, Symmetry is designed for chat, but it could be used for other purposes in the future (e.g., autocomplete).

3. **Q: How does Symmetry ensure data privacy?**
   A: Symmetry uses encrypted connections for all communications. After initial matchmaking, clients and providers communicate directly, bypassing the central server. However, providers do have access to decrypted data for processing, so consider data sensitivity when using the network.

4. **Q: Can I use Symmetry in my own projects?**
   A: Yes! The Symmetry project is open source, and you can use it in your own projects.

5. **Q: Are there rewards for being a provider?**

- Rewards will be in the form of tokens on the SOL blockchain, which will be used to pay providers for their services.
- Providers will be able to earn rewards by providing data to clients.
- A POW algorithm will be implemented, which will ensure that the network is secure and reliable.

1. **Q: How can I stay updated on Symmetry's development?**
   A: Keep an eye on the official Symmetry GitHub repository and documentation for the latest updates and announcements.

By exploring Symmetry, whether as a user through the twinny extension or as a provider, you're participating in the development of distributed computing technologies. As Symmetry evolves, it aims to offer more flexible and powerful options for developers and researchers alike.

Please refer to the [privacy policy](https://www.twinny.dev/privacy) for information regarding usage of the network.
