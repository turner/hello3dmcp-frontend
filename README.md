# Hello3DMCP Frontend

A fully functional standalone Three.js 3D visualization application that has been adapted to be driven by the [hello3dmcp-server](https://github.com/aidenlab/hello3dmcp-server) via WebSocket.

**Primary Use:** This frontend is designed to be controlled by Claude through the MCP server, enabling real-time 3D model manipulation via natural language commands.

**Standalone Capability:** While intended for MCP server control, the application can also be built and run independently as a traditional Three.js application with full interactive controls.

## Application Overview

![Hello3DMCP Frontend Application](readme_img/hello3dmcp-frontend-figure.png)

The application features interactive controls for the 3D model and lighting setup:

- **Model**: The 3D model can be rotated and zoomed using mouse/touch controls. Click and drag to rotate, scroll to zoom.

- **Fill Light**: The rectangle outline represents the bounds of the area light. Users can directly grab and drag the area light to reposition it, and zoom in/out to adjust its distance from the model.

- **Key Light**: Similar to the fill light, the rectangle outline represents the bounds of the area light. Users can grab and drag the area light to reposition it, and zoom in/out to control its distance relative to the model.

---

## Quick Start

**Requirements:** Node.js v18+, npm

```bash
npm install
npm run dev
```

Open `http://localhost:5173` to run the application in standalone mode.

---

## Usage with MCP Server

This frontend is designed to be driven by the [hello3dmcp-server](https://github.com/aidenlab/hello3dmcp-server). **All interaction in MCP mode initiates via Claude:**

1. **Start the MCP server** (see [hello3dmcp-server README](https://github.com/aidenlab/hello3dmcp-server))
2. **In Claude Desktop**, ask Claude: "Get Hello3D URL" (or similar command)
3. **Claude responds** with a URL containing your unique session ID
4. **Click the provided URL** to launch the frontend application in your browser
5. **The frontend connects** to the MCP server via WebSocket using the session ID
6. **Control the 3D model** by asking Claude to manipulate it

The frontend receives commands via WebSocket and updates the 3D scene in real-time. In this integrated mode (server + frontend), all interaction flows through Claude.

---

## Standalone Usage

The application can be used independently as a pure frontend application with no MCP server involved:

```bash
npm install
npm run dev
```

Open `http://localhost:5173` and interact with the 3D model using mouse/touch controls. In standalone mode, there is no WebSocket connection or MCP server interaction.

---

## Production Build

```bash
npm run build      # Creates optimized dist/ folder
npm run preview    # Preview the production build locally
```

### Netlify Deployment

| Setting | Value |
|---------|-------|
| Build command | `npm run build` |
| Publish directory | `dist` |
| Environment variable | `VITE_WS_URL=ws://localhost:3001` |

---

## Project Structure

```
src/
├── Application.js        # Main app + WebSocket integration
├── SceneManager.js       # Scene & model manipulation
├── WebSocketClient.js    # Server communication
├── Model.js              # Model class
├── CameraController.js   # Camera controls
├── RotationController.js # Rotation handling
├── AreaLight.js          # Lighting
├── RayPicker.js          # Click/touch interactions
├── InteractionModeManager.js
├── constants.js
├── main.js               # Entry point
├── style.scss
└── utils/
    ├── color/
    └── coordinates/

public/models/            # 3D model assets
```

---

## Related

- [hello3dmcp-server](https://github.com/aidenlab/hello3dmcp-server) — The MCP server that controls this frontend

---

## License

MIT — Contributions welcome!
