## PhotoshopEvents (CEP Sample)

- [中文说明](readme_zh.md)

This sample shows how to listen to Photoshop events from a CEP panel. It registers a few common events in `host/ps.jsx` and uses `js/CSInterface.js` to communicate with Photoshop.

### Supported hosts
- Photoshop (PHXS)

### Prerequisites
- Enable loading unsigned CEP extensions (Windows): run `enable_cep_debug.reg` in the project root.
- Ensure the folder contains `CSXS/manifest.xml`.

### Install
1. Copy the entire `PhotoshopEvents` folder to the CEP extensions folder.
   - Windows: `C:\Users\<YOUR_USER>\AppData\Roaming\Adobe\CEP\extensions\PhotoshopEvents`
2. Restart Photoshop.
3. Open: Window → Extensions → “PhotoshopEvents” or “PhotoshopEvents 2”.

### Debugging
- Remote DevTools:
  - `.debug` maps extension IDs to ports (8001, 8002).
  - Open a browser to `http://localhost:8001/` (or `8002`) to attach DevTools.
- Inspect errors:
  - Use DevTools Console for JavaScript errors.
  - Use Network and Sources panels for requests and breakpoints.
  - When calling `CSInterface.evalScript()`, check the callback result string for ExtendScript errors.

### Development flow
- No build step is required; edit HTML/CSS/JS directly.
- To apply changes, close and reopen the panel (or restart Photoshop if needed).

### Packaging (optional)
- For distribution as `.zxp`, sign with Adobe ZXPSignCmd (not included in this repo).
- During development, the provided registry file enables loading without signing.

### Files of interest
- `CSXS/manifest.xml` — extension metadata, hosts, UI, icons.
- `host/ps.jsx` — Photoshop event listeners and ExtendScript glue.
- `js/CSInterface.js` — CEP bridge API.
