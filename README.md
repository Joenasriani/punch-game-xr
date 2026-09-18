# Stress Buster 3000 — WebXR Edition

A browser-based augmented-reality interaction experiment built with Three.js and WebXR.

This repository is a separate WebXR implementation from the non-XR `punch-game` project. It renders an image target in AR space and detects punch-like contact using tracked hand joints.

## Features

- WebXR augmented-reality session support
- Required WebXR hand tracking
- Optional DOM overlay support
- Two tracked XR hands
- Fingertip-to-target proximity detection
- Selectable image targets
- Runtime texture replacement
- Procedural impact particles
- Target scale feedback on contact
- Synthesized punch sound using the Web Audio API
- Responsive Three.js rendering

## Implementation

The project is implemented as a single-page browser application in `index.html`.

- **Three.js 0.160.0** is loaded as an ES module from Skypack.
- **ARButton** creates and manages the WebXR AR-session entry control.
- **WebXR hand tracking** is requested as a required session feature.
- **DOM Overlay** is requested as an optional feature for the in-session target selector.
- **Web Audio API** generates the impact sound at runtime.
- **Tailwind CSS** is loaded from the CDN for interface styling.

The AR target is a textured `THREE.CircleGeometry` positioned in front of the viewer. During each XR frame, the application checks the index-finger-tip joint, falling back to the middle-finger-tip joint, for both tracked hands. A hit is registered when a tracked fingertip enters the configured distance threshold and the punch cooldown has elapsed.

On contact, the application plays the synthesized sound, spawns short-lived sphere particles with simple gravity, and briefly scales the target group.

## Requirements

Running the AR mode requires:

- a browser with WebXR AR support;
- a device/browser combination that supports WebXR hand tracking;
- a secure HTTPS context for WebXR session access.

Feature availability depends on the browser and device. The page displays an AR start control only when the required WebXR capabilities are available.

## Running

No build step is defined in the repository.

Serve the repository over HTTPS with a static web server and open `index.html` on a compatible device.

## Repository Structure

```text
.
└── index.html
```

The HTML file contains the UI, module imports, Three.js scene setup, WebXR session configuration, hand-joint interaction logic, particle behavior, audio generation, and render loop.
