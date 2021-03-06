<p align="center">
  <img width="750" src="https://user-images.githubusercontent.com/678665/45566726-404d9e80-b860-11e8-94b6-527dfcc3b3b3.png">
</p>

# Vuex Electron

[![Travis](https://img.shields.io/travis/com/vue-electron/vuex-electron.svg?style=for-the-badge&longCache=true)](https://travis-ci.com/vue-electron/vuex-electron)
[![Code Climate](https://img.shields.io/codeclimate/maintainability/vue-electron/vuex-electron.svg?style=for-the-badge&longCache=true)](https://codeclimate.com/github/vue-electron/vuex-electron)
[![Code Climate](https://img.shields.io/codeclimate/coverage/vue-electron/vuex-electron.svg?style=for-the-badge&longCache=true)](https://codeclimate.com/github/vue-electron/vuex-electron)
[![Code Style Prettier](https://img.shields.io/badge/code%20style-prettier-brightgreen.svg?style=for-the-badge&longCache=true)](https://github.com/prettier/prettier)
[![Made With Love](https://img.shields.io/badge/made%20with-love-brightgreen.svg?style=for-the-badge&longCache=true)](https://github.com/MrEmelianenko)

The easiest way to share your Vuex Store between all processes (including main).

### Fork

This fork contains the following modifications:
- properly initialize state when creating a new renderer process and when not using persistent state
- allow renderer processes to commit mutations

### Features

:star: Persisted state  
:star: Shared mutations

### Requirements

- [Vue](https://github.com/vuejs/vue) v2.0+
- [Vuex](https://github.com/vuejs/vuex) v2.0+
- [Electron](https://github.com/electron/electron) v2.0+

### Installation

Installation of the Vuex Electron easy as 1-2-3.

1. Install package with using of [yarn](https://github.com/yarnpkg/yarn) or [npm](https://github.com/npm/cli):

    ```
    yarn install vuex-electron
    ```

    or

    ```
    npm install vuex-electron
    ```

2. Include plugins in your Vuex store::

    ```javascript
    import Vue from "vue"
    import Vuex from "vuex"

    import { createPersistedState, createSharedMutations } from "vuex-electron"

    Vue.use(Vuex)

    export default new Vuex.Store({
      // ...
      plugins: [
        createPersistedState(),
        createSharedMutations()
      ],
      // ...
    })
    ```

3. In case if you enabled `createSharedMutations()` plugin you need to create an instance of store in the main process. To do it just add this line into your main process (for example `src/main.js`):

    ```javascript
    import './path/to/your/store'
    ```

4. Well done you did it! The last step is to add the star to this repo :smile:

**Usage example: [Vuex Electron Example](https://github.com/vue-electron/vuex-electron-example)**

### Options

Available options for `createPersistedState()`

```javascript
createPersistedState({
  whitelist: ["whitelistedMutation", "anotherWhitelistedMutation"],

  // or

  whitelist: (mutation) => {
    return true
  },

  // or

  blacklist: ["ignoredMutation", "anotherIgnoredMutation"],

  // or

  blacklist: (mutation) => {
    return true
  }
})
```

Available options for `createSharedMutations()`

```javascript
createSharedMutations({
  syncStateOnRendererCreation: true
})
```

`syncStateOnRendererCreation: true` will synchronize the main process's Vuex state with a renderer when it's created.
Use it when `createPersistedState()` isn't used to make sure the states are synchronized (else you might end up with a different state between a renderer and the main process).

### Warning

Vuex-electron uses ipc to share actions and mutations between processes, so the Vuex state is subject to the same limitations that ipc has, most notably the fact that data is serialized through JSON before being sent.

### Authors

Andrew Emelianenko  
IG: [@truemelianenko](https://www.instagram.com/truemelianenko)

Modified by Jean Moreno for SyncSketch LLC

### License

[MIT License](https://github.com/vue-electron/vuex-electron/blob/master/LICENSE)
