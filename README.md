# MCP postMessage Transport Reference Implementation

This is a reference implementation for a **proposed new transport** for the Model Context Protocol (MCP) that enables zero-installation, browser-native MCP servers. The postMessage transport allows MCP servers to run directly in web browsers (iframes/popups) and communicate with clients using the browser's `window.postMessage` API, eliminating installation requirements while enabling rich interactive tools.

**🌐 [Try the Live Demo](https://joshuamandel.com/mcp-postmessage)**

📋 **[Read the Complete Protocol Specification](src/protocol/README.md)** for detailed technical documentation, message formats, and security requirements.

** [Read the proposal on modelcontextprotocol](https://github.com/modelcontextprotocol/modelcontextprotocol/issues/1005)

## 🚀 Quick Start

### Prerequisites
- [Bun](https://bun.sh) installed
- Modern web browser

### Running the Demo

1. **Install dependencies:**
   ```bash
   bun install
   ```

2. **Start the demo:**
   ```bash
   bun run dev
   ```
   This starts the demo server.

### Building for Production

1. **Build the complete demo application:**
   ```bash
   bun run build
   ```
   This creates a `dist/` folder with all assets bundled for deployment.

2. **Preview the built application:**
   ```bash
   bun run preview
   ```

3. **Deploy to GitHub Pages:**
   The repository includes GitHub Actions that automatically deploy to GitHub Pages on push to main branch.
   ```

4. **Open your browser:**
   - Client: http://localhost:3000
   - Pi Calculator: http://localhost:3001

## 🎯 Demo Instructions

1. **Open the client** at http://localhost:3000
2. **Add the Pi Calculator server** (should be pre-configured):
   - URL: `http://localhost:3001#setup`
3. **Click "Setup"** to configure the server
4. **Click "Connect"** to establish MCP connection
5. **Try the interactive Pi calculation** with Monte Carlo visualization

## 📋 What This Demonstrates

### postMessage Transport Features
- **Zero Installation**: Servers run directly in browser
- **Two-Phase Protocol**: Setup → Transport phases
- **Security**: Origin validation and message routing
- **Visibility Control**: Optional/required/hidden server UI

### Pi Calculator Server
- **MCP Tool**: `calculate_pi` method with configurable iterations
- **Interactive UI**: Real-time Monte Carlo visualization
- **Progressive Calculation**: Live progress updates
- **Canvas Visualization**: Points plotted inside/outside unit circle

## 🏗️ Architecture

```
├── src/
│   ├── client/           # Client transport implementation
│   ├── server/           # Server transport implementation
│   ├── types/            # TypeScript interfaces
│   └── utils/            # Helper functions
├── demo-client/          # React-based demo client
└── servers/
    └── pi-calculator/    # Monte Carlo Pi calculator server
```

## 🔧 Developing

### Prerequisites
- [Bun](https://bun.sh) installed
- Modern web browser

### Development Commands

```bash
# Install dependencies
bun install

# Type checking
bun run type-check

# Build for production
bun run build

# Start individual components
bun run demo:client    # Client on port 3000
bun run demo:pi       # Pi Calculator on port 3001

# Start complete demo (client + Pi server)
bun run demo
```

## 📖 Protocol Overview

The postMessage transport implements a two-phase connection model:

1. **Setup Phase** (`#setup` parameter):
   - Server announces readiness
   - Client performs handshake
   - User completes configuration
   - Server reports setup completion

2. **Transport Phase** (normal URL):
   - Server announces transport readiness
   - Client establishes MCP connection
   - Standard MCP protocol communication

## 🛡️ Security

- **Origin Validation**: All messages validated against allowed origins
- **Message Routing**: Proper postMessage target origin handling
- **Iframe Sandboxing**: Secure execution environment
- **No Ambient Authority**: Explicit connection handshakes required

## 📝 License

MIT License - see LICENSE file for details.
