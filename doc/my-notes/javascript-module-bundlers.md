# JavaScript Module Bundlers ([Source](https://snipcart.com/blog/javascript-module-bundler))

[Fireship - Module Bundlers Explained (Video)](https://www.youtube.com/watch?v=5IG4UmULyoA)

## What is a js module bundler?

- A bundler is a development tool that combines many JavaScript code files into a single one that is production-ready loadable in the browser

- A fantastic feature of a bundler is that it generates a dependency graph as it traverses your first code files. This implies that beginning with the entry point you specified, the module bundler keeps track of both your source files’ dependencies and third-party dependencies. This dependency graph guarantees that all source and associated code files are kept up to date and error-free.

## How does bundlers work?

- A bundler's operation is divided into two stages:
  - Dependency graph generation
  - Eventual bundling.

### Mapping a Dependency Graph

The first thing a module bundler does is generate a relationship map of all the served files. This process is called Dependency Resolution. To do this, the bundler requires an entry file which should ideally be your main file. It then parses through this entry file to understand its dependencies.

- It enables the module to construct a dependency order, vital for retrieving functions when a browser requests them.
- It prevents naming conflicts since the JS bundler has a good source map of all the files and their dependencies.
- It detects unused files allowing us to get rid of unnecessary files.

### Bundling

After receiving inputs and traversing its dependencies during the Dependency Resolution phase, a bundler delivers static assets that the browser can successfully process. This output stage is called Packing. During this process, the bundler will leverage the dependency graph to integrate our multiple code files, inject the required function and module.exports object, and return a single executable bundle that the browser can load successfully.

## JavaScript Module Bundlers

- Examples : webpack, esbuild, parcel, rollup, browserify

### Webpack

- The most popular JavaScript module bundler.
- To understand how it performs the dependency resolution step, you must first grasp these 6 concepts

1. Entry

- Specifies where Webpack should initiate its dependency graph. You can have one or more entry points depending on your app’s architecture. Webpack iterates through the module(s) listed in the webpack.config.js config file identifying the entry point’s direct and indirect dependencies.

  `module.exports = {  entry: './app/index.js',  };`

2. Output

- Specifies the desired destination for the final output after Webpack completes the packing process. The Output property contains two sub-values: the file path, usually the `/dist` folder, and the desired `filename`.

```js
const path = require('path');
module.exports = {
  entry: './app/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'webpack-app.bundle.js',
  },
};
```

3. Loaders : Allow Webpack to transform and bundle non-JS files.

4. Plugins : Allow Webpack to perform more advanced actions like custom resource optimization and management.

5. Mode : Allows Webpack to configure its operations to production or development modes dynamically.

6. Browser Compatibility : Allow Webpack to build bundles that support modern and old browsers with features like promises and polyfills.
