<div align="center">
  <a href="https://github.com/webpack/webpack">
    <img width="200" height="200" src="https://webpack.js.org/assets/icon-square-big.svg">
  </a>
</div>

[![npm version](https://badge.fury.io/js/css-fix-url-loader.svg)](https://badge.fury.io/js/css-fix-url-loader) [![npm module downloads](https://img.shields.io/npm/dt/css-fix-url-loader.svg)](https://npmjs.org/package/css-fix-url-loader) [![Dependency Status](https://david-dm.org/studio-webb/css-fix-url-loader.svg)](https://david-dm.org/studio-webb/css-fix-url-loader) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

# css-fix-url-loader 

Webpack loader to transform URLs to other URLs in CSS.
Fork from [css-url-loader](https://github.com/keidrun/css-url-loader/)

## Description

Transform URLs to other URLs in the `url()`s in your CSS. You can change relative urls
to absolute urls, or absolute urls to relative urls, or you can change old urls to new urls that you want.

## Install

```bash
npm install --save-dev css-fix-url-loader
```

Or

```bash
yarn add --dev css-fix-url-loader
```

## Usage

### When you want to trasform `url(/assets/...)` to `url(https://domain/assets/...)`, the `webpack.config.js` is below

```javascript
module.exports = {
  ...
  module: {
    rules: [
      ...
      {
        test: /\.css$/,
        use: ExtractTextPlugin.extract({
          fallback: 'style-loader',
          use: [
            'css-loader',
            {
              loader: 'css-fix-url-loader',
              query: {
                from: '/assets/',
                to: 'https://domain/assets/'
              }
            }
          ],
        }),
      },
      ...
    ],
  },
  plugins: [
    ...
    new ExtractTextPlugin('bundle.css'),
    ...
  ],
```

### When you want to trasform `url(/assets/...)` to `url(/dir/assets/...)`, the `webpack.config.js` is below

```javascript
module.exports = {
  ...
  module: {
    rules: [
      ...
      {
        test: /\.css$/,
        use: ExtractTextPlugin.extract({
          fallback: 'style-loader',
          use: [
            'css-loader',
            {
              loader: 'css-fix-url-loader',
              query: {
                from: '/assets/',
                to: '/dir/assets/'
              }
            }
          ],
        }),
      },
      ...
    ],
  },
  plugins: [
    ...
    new ExtractTextPlugin('bundle.css'),
    ...
  ],
```

### When you want to trasform urls when only development, the `webpack.config.js` is below

```javascript
module.exports = {
  ...
  module: {
    rules: [
      ...
      {
        test: /\.css$/,
        use: ExtractTextPlugin.extract({
          fallback: 'style-loader',
          use: [
            'css-loader',
            {
              loader: 'css-fix-url-loader',
              query: {
                from: '/assets/',
                to: '/tmp/assets/',
                env: 'development'
              }
            }
          ],
        }),
      },
      ...
    ],
  },
  plugins: [
    ...
    new ExtractTextPlugin('bundle.css'),
    ...
  ],
```

### When you want to trasform urls from absolute to relative, the `webpack.config.js` is below

```javascript
module.exports = {
  ...
  module: {
    rules: [
      ...
      {
        test: /\.css$/,
        use: ExtractTextPlugin.extract({
          fallback: 'style-loader',
          use: [
            'css-loader',
            {
              loader: 'css-fix-url-loader',
              query: {
                from: '/images',
                to: path.resolve(__dirname, './src/images'),
                relative: true
              }
            }
          ],
        }),
      },
      ...
    ],
  },
  plugins: [
    ...
    new ExtractTextPlugin('bundle.css'),
    ...
  ],
```

## Options

| Option   | Description                                                                             | Required |
| -------- | :-------------------------------------------------------------------------------------- | :------: |
| from     | original url in url()                                                                   |    Y     |
| to       | transformed url                                                                         |    Y     |
| env      | value to control execution timing with `process.env.NODE_ENV`. Default is 'production'. |    N     |
| relative | if need to trasform urls from absolute to relative                                      |    N     |

