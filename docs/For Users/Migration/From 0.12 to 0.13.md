# Migrate from 0.12 to 0.13 {: doctitle}
---

[TOC]

## Architecture Changes

1. If NW.js is running under [Mixed Context Mode](../Advanced/JavaScript Contexts in NW.js.md#mixed-context-mode) (boot NW.js with `--mixed-context` argument), `nw.*` is kind of mirror of `window.*`. In this mode, you **CANNOT** share variables among frames or windows by assigning it to Node context. So do **NOT** turn on Mixed Context mode if your application is heavily depending on this variable sharing feature.

## Node.js Changes

1. Node.js is bumped to 5.x in latest build. Check your NPM modules to make sure they support Node.js 5.x **especially for native modules**. There is [a list of native modules](https://github.com/nodejs/node/issues/2798) which should be migrated to latest NaN 2.

## API Changes

1. Different build flavors support different set of APIs and capabilities. See [Build Flavors](../Advanced/Build Flavors.md) to choose the right NW.js flavor or [build your own](../../For Developers/Building NW.js.md).
2. `Shortcut` API does **NOT** map <kbd>Ctrl</kbd> modifier to <kbd>&#8984;</kbd> on Mac OS X. However 0.13.0 supports `Command` modifier in cross platform way. So it's your responsible to detect the OS and choose the right modifier when registering hotkeys. See [Shortcut.key](../../References/Shortcut.md#shortcutkey) for details.
3. `single-instance` in [manifest file](../../References/Manifest Format.md#single-instance) is **deprecated** and it's always `true`. You **CANNOT** have multiple instances for your app.
4. `toolbar` in [manifest file](../../References/Manifest Format.md#toolbar) is **deprecated** and it's always `false`. The traditional toolbar will **NOT** be supported including the reload buttons, location bar and DevTools buttons. As a workaround, you can open / close DevTools with <kbd>F12</kbd> (Windows & Linux) or <kbd>&#8984;</kbd>+<kbd>&#8997;</kbd>+<kbd>i</kbd> (Mac). And use [`win.reload()`](../../References/Window.md#winreload) and [`win.reloadDev()`](../../References/Window.md#winreloaddev) to simulate the reload buttons.
5. `no-edit-menu` in [manifest file](../../References/Manifest Format.md#no-edit-menu-mac) is **deprecated**.
6. Event `capturepagedone` of [`Window` API](../../References/Window.md#event-capturepagedone) is **deprecated**. Use the callback with the [`win.capturePage(callback [, config ])`](../../References/Window.md#wincapturepagecallback--config-) instead.