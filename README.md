# @rubys/snowpack-plugin-require-context

A Snowpack plugin implementing webpack's
[require.context](https://webpack.js.org/guides/dependency-management/#requirecontext)
API.  The motivation for this was to bring the simplicity of
[Webpack's development of Stimulus applications](https://stimulus.hotwire.dev/handbook/installing#using-webpack)
to Snowpack, but it should be useful for other purposes too.

This plugin works by rewriting `require.context` calls to generate the
necessary context definitions at build time.  It will also watch the
source directories for changes and trigger a rebuild when files change.

The `input` configuration option described below is optional, and if not
present will cause all `.js` files to be scanned.  Only those that contain
calls to `require.context` will be processed by this plugin.

Limitations of this implementation:
 * fourth argument to `require.context` (`sync`) is ignored/not supported
 * resulting context object only has a `keys` property, in other words
    * it has no `resolve` function
    * it has no `id` property
 * module definitions does not contain named exports, only `default`

None of these limitations affect Stimulus.js usage.

Usage:

```bash
npm install @rubys/snowpack-plugin-require-context
```

Then add the plugin to your Snowpack config:

```js
// snowpack.config.js

module.exports = {
  plugins: [
    [
      '@rubys/snowpack-plugin-require-context',
      {
        input: ['application.js'], // files to watch
      },
    ],
  ],
};
```

## Plugin Options

| Name     |    Type    | Description
|
| :------- | :--------: |
:-------------------------------------------------------------------------- |
| `input`  | `string[]` | Array of extensions to watch for.
