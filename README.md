# DMT App Bundler
Integration point for DMT Apps (frontends)

## Core concepts

### ● DMT Frontend

DMT Frontend is a Single Page App built with `DMT App Bundler` which bundles all core DMT Apps together (Search, Meet, Insight, Player, Clock ...).

Core apps are available at `/view/${coreApp}`. Bundler provides some common app structure and layout (for example sidebar with device name and time) and color variables / theming.

Separate bundles (not yet bundled apps for development and testing / user apps) are loaded from subroutes `/apps/{appName}` and are separate bundles.

### ● DMT APP

DMT APP is a separate npm package containing a Svelte component which Bundler imports at compile time.

Component receives a `ConnectedStore` instance as a prop. ConnectedStore is a Svelte-compatible store which always has the up-to-date `dmt-proc` state.

We can also run each DMT APP in **standalone mode** while developing (eg. `/apps/{appName}`). In this case app initializes `ConnectedStore` instance in `main.js`.

## Considerations

### Device-dependent initial (home) screen

Initial screen visible when opening the DMT Frontend will differ depending on device type:

- Personal Computer
- Personal Server
- Single Board Compuer (Personal / Home Tablet)

It is now quite likely that the best approach would be to compile 3 different bundles, one for each platform type.

There may be a lot of frontend code that is not useful / needed on Tablets (for example upcoming `LinkManager` for collecting and annotating weblinks) and the entire IoT part does not make sense on Servers.

### An example of different bundles configuration approach

```
frontend: computer
  app: clock
  app: search
  app: player
  app: insight
  app: draw

frontend: server
  app: search
  app: insight
  app: draw

frontend: raspberry
  app: clock
  app: player
  app: draw
```

**[ TO BE CONTINUED ... ]**
