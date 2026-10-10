# Rust Desktop Environment

## 1. Project Vision

Build a minimal, performance-conscious, Arch Linux-inspired desktop environment that runs in a web browser and is distributed as one standalone HTML file.

The project takes inspiration from Arch Linux, Wayland, Hyprland, and Linux ricing culture. It should prioritize keyboard-driven workflows, tiling window management, a useful terminal, modular applications, and deep customization.

This is a functional software project, not a static desktop mockup or a CSS theme.

The objective is to recreate the useful desktop experience within browser constraints, not to claim that the project is an actual Linux distribution.

## 2. Core Technology

- **Rust:** Primary implementation language for desktop logic, window management, workspace state, terminal commands, configuration, application management, and other suitable system components.
- **WebAssembly:** Compile the Rust application to WASM for browser execution.
- **Rust UI framework:** Select a framework capable of rendering the desktop through Rust with minimal manually authored HTML, CSS, and JavaScript. Evaluate browser compatibility, performance, maturity, and bundling requirements before choosing.
- **HTML applications:** Desktop applications may be distributed as individual HTML files fetched from a designated GitHub repository.
- **Build tooling:** Use only the additional languages and tools required to compile, bundle, test, and distribute the project reliably.

Do not implement the desktop interface as a conventional JavaScript application with Rust added superficially.

Minimal generated HTML or JavaScript glue is acceptable if technically necessary. The desktop's behavior and primary interface must be implemented in Rust wherever practical.

HTML application files are an intentional exception because they are the chosen format for third-party or modular applications.

## 3. Desktop Functionality

The desktop must eventually support:

- Window creation, closing, focusing, resizing, and movement.
- Tiling and floating windows.
- Multiple virtual workspaces.
- Keyboard-driven window and workspace management.
- Configurable layouts inspired by Hyprland, including master-stack and dwindle-style arrangements.
- Window rules, gaps, borders, and focus behavior.
- An application launcher and application registry.
- Persistent desktop configuration.
- Proper input handling and predictable state management.

Implement actual window-management logic. Do not simulate functionality with decorative buttons or hardcoded screenshots.

## 4. Terminal

Provide a built-in terminal with a Rust-based command interpreter.

The terminal must execute real commands supported by the desktop environment and return truthful output.

Planned capabilities include:

- Help and command discovery.
- Application listing, installation or import, launching, and removal.
- Workspace switching and management.
- Window layout and configuration management.
- Theme, wallpaper, and ricing configuration.
- Application repository discovery and updates.
- Useful diagnostics and system information about the desktop itself.

Commands should have documented syntax, meaningful errors, and testable effects.

Do not pretend that arbitrary Linux shell commands, native processes, package installation through pacman, or kernel operations work in a browser where they are not actually available.

Keep the command system extensible without introducing unnecessary abstractions.

## 5. HTML Application System

Applications are individual `.html` files hosted in a designated GitHub repository.

The eventual application system should support:

- Discovering applications through a repository manifest.
- Displaying application names, descriptions, versions, and other useful metadata.
- Fetching an application when requested rather than downloading every application at startup.
- Opening applications inside desktop-managed windows.
- Maintaining independent application document state.
- Closing and reopening applications.
- Handling unavailable repositories, network errors, malformed manifests, and incompatible versions.
- Providing a documented interface for applications to interact with permitted desktop features.
- Applying appropriate security isolation and explicit permission boundaries to untrusted applications.

Keep application source files separate during development.

Treat remotely fetched HTML and JavaScript as untrusted code. Do not give third-party applications unrestricted access to desktop internals, credentials, or other applications.

The app system must respect browser origin policies, sandbox restrictions, storage limitations, and network security.

## 6. Ricing and Customization

Ricing is a major part of the project, but it comes after the functional foundations.

Planned customization includes:

- Color schemes and themes.
- Wallpapers and backgrounds.
- Fonts and typography.
- Window borders, gaps, rounding, and animations.
- Panels, bars, widgets, and desktop indicators.
- Tiling layouts and window behavior.
- Keyboard bindings and window rules.
- Importing, exporting, and sharing configuration profiles.

Customization must affect actual desktop behavior and appearance through a coherent configuration system. Avoid scattering hardcoded values throughout the codebase.

## 7. Performance and Minimal Dependencies

Performance and simplicity are priorities.

- Prefer small, reliable, actively maintained dependencies.
- Avoid unnecessary frameworks and duplicated functionality.
- Load applications and resources on demand.
- Avoid blocking the UI with expensive work.
- Minimize unnecessary allocations and redundant state.
- Handle errors explicitly rather than silently ignoring them.
- Measure performance where possible instead of making unsupported performance claims.
- Do not add speculative features before the foundations work.

Do not optimize prematurely at the expense of correctness or maintainability.

## 8. Single-HTML Distribution

The final production artifact must be one standalone HTML file.

It must contain the compiled WASM and all required runtime assets, including any generated JavaScript glue and bundled default application assets.

The core desktop must start without a development server, separately hosted runtime files, a CDN, or external assets.

The desktop's core functionality should be available offline wherever browser capabilities permit. Discovering or downloading applications from GitHub requires network access.

Support a development workflow with normal source files and build artifacts kept separate from the final single-file distribution.

The build process must verify that the WASM and required assets are actually embedded in the final artifact.

Test the exported HTML independently of the development server. Do not assume that a successful development preview proves that the single-file build works.

## 9. Technical Boundaries

This is a browser-hosted environment, not a native Linux system.

Do not claim to implement native Wayland protocols, Linux kernel features, native process execution, unrestricted filesystem access, or native package management unless a real supported mechanism exists.

Use browser APIs honestly and document their limitations.

The browser's rendering engine may be used internally to render isolated HTML applications. This does not change the requirement that the desktop itself be implemented primarily in Rust.

## 10. Development Rules

- Inspect the existing repository before making changes.
- Work in small, independently testable milestones.
- Never rewrite unrelated files without a clear reason.
- Avoid unnecessary dependencies and boilerplate.
- Do not implement future milestones prematurely.
- Do not claim that untested features work.
- Report actual test results and remaining limitations.
- Keep explanations and command output concise.
- Preserve working functionality when adding features.
- Prefer reversible, incremental changes.
- Verify each milestone before proceeding to the next.

## 11. Initial Development Order

1. Audit the repository and choose the technical architecture.
2. Establish a minimal Rust-to-WASM build and UI.
3. Implement the desktop's core state and window management.
4. Add workspaces, keyboard controls, and tiling layouts.
5. Build the terminal and desktop command system.
6. Implement GitHub-based HTML application discovery and loading.
7. Add configuration, ricing, and persistence.
8. Implement and verify the complete single-HTML production build.
9. Expand functionality incrementally based on actual needs.

This order is a roadmap, not permission to implement all milestones at once.

## 12. Guiding Principle

Build the system first. Rice it afterward.

Prefer working features, precise behavior, security, performance, and maintainable Rust code over superficial visual polish or unnecessary