### Webpack Concepts
At its core, webpack is a static module bundler for modern JavaScript applications. When webpack processes your application, it internally builds a dependency graph from one or more entry points and then combines every module your project needs into one or more bundles, which are static assets to serve your content from.


## Entry
An entry point indicates which module webpack should use to begin building out its internal dependency graph. Webpack will figure out which other modules and libraries that entry point depends on (directly and indirectly).

By default its value is ./src/index.js, but you can specify a different (or multiple) entry points by setting an entry property in the webpack configuration: For example:

# webpack.config.js

module.exports = {
  entry: './path/to/my/entry/file.js',
};


## Output
The output property tells webpack where to emit the bundles it creates and how to name these files. It defaults to ./dist/main.js for the main output file and to the ./dist folder for any other generated file.

You can configure this part of the process by specifying an output field in your configuration:

# webpack.config.js

const path = require('path');

module.exports = {
  entry: './path/to/my/entry/file.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'my-first-webpack.bundle.js',
  },
};
In the example above, we use the output.filename and the output.path properties to tell webpack the name of our bundle and where we want it to be emitted to. In case you're wondering about the path module being imported at the top, it is a core Node.js module that gets used to manipulate file paths.


## Loaders
Out of the box, webpack only understands JavaScript and JSON files. Loaders allow webpack to process other types of files and convert them into valid modules that can be consumed by your application and added to the dependency graph.

At a high level, loaders have two properties in your webpack configuration:

The test property identifies which file or files should be transformed.
The use property indicates which loader should be used to do the transforming.

# webpack.config.js

const path = require('path');

module.exports = {
  output: {
    filename: 'my-first-webpack.bundle.js',
  },
  module: {
    rules: [{ test: /\.txt$/, use: 'raw-loader' }],
  },
};
The configuration above has defined a rules property for a single module with two required properties: test and use. This tells webpack's compiler the following:

# "Hey webpack compiler, when you come across a path that resolves to a '.txt' file inside of a require()/import statement, use the raw-loader to transform it before you add it to the bundle."