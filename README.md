# Hello3DMCP Frontend

A Three.js visualization app that lets Claude control 3D models in real-time via MCP.

**Features:** Interactive rotation/zoom • Real-time MCP updates

---

## Quick Start

**Requirements:** Node.js v18+, npm, and the [hello3dmcp-server](https://github.com/aidenlab/hello3dmcp-server) running

```bash
npm install
npm run dev
```

Open `http://localhost:5173` — the app auto-connects to the MCP server at `ws://localhost:3001`.

---

## Production

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

## WebSocket Protocol

### Registration
On connect, the frontend registers its session:
```json
{ "type": "registerSession", "sessionId": "<session-id>" }
```

### Commands (Server → Frontend)
`changeColor` · `changeSize` · `scaleModel` · `changeBackgroundColor` · `setKeyLightIntensity` · `setKeyLightColor` · [more in MCP server docs]

### State Queries
Server requests state:
```json
{ "type": "requestState", "requestId": "<id>", "forceRefresh": false }
```

Frontend responds:
```json
{ "type": "stateResponse", "requestId": "<id>", "state": { ... } }
```

---

## Development

1. Start the [MCP server](https://github.com/aidenlab/hello3dmcp-server)
2. Run `npm run dev`
3. Open `http://localhost:5173?sessionId=<your-session-id>`

---

## Troubleshooting

| Problem | Check |
|---------|-------|
| **WebSocket won't connect** | MCP server running on port 3001? Correct session ID? Browser console errors? |
| **Changes not appearing** | WebSocket connected? Session ID matches? Server sending commands? |

---

## Related

- [hello3dmcp-server](https://github.com/aidenlab/hello3dmcp-server) — The MCP server that controls this frontend

---

## License

MIT — Contributions welcome!
