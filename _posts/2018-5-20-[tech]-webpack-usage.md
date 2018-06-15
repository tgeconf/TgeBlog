<style>
  p{
    margin: .5em;
  }
</style>
<h2>What is Webpack</h2> 
<p>Webpack is a <b>module hundler</b>. It can be used to bundle your scripts, images, or styles.

<h2>Start to Use Webpack</h2>
<h4>Installation</h4>
<p>using npm to install
<pre style="background: #eee">npm install -g webpack</pre>

<h4>Bundle JS files</h4>
<ol>
  <li>
    Generate package.json:<br/>
    <pre style="background: #eee">npm init</pre>
    then we add <b><i>scripts</i></b> in the end of package.json:
    <pre style="background: #eee">
      "scripts":{
        "dev":"cross-env NODE_ENV=development webpack",
        "opt":"cross-env NODE_ENV=production webpack"
      }
    </pre>
  </li>
  <li>
    install webpack as the dependent package<br/>
    <pre style="background: #eee">npm install --save-dev webpack</pre>
  </li>
  <li>
    create two folders <b><i>src</i></b> and <b><i>public</i></b>, <b><i>src</i></b> is for the JS modules we are going to write and <b><i>public</i></b> is for the packed JS file.
  </li>
  <li>
    create <b><i>webpack.config.js</i></b> as the conf file to export JS file. This is my <b><i>webpack.config.js</i></b>:
    <pre style="background: #eee">
      var webpack = require('webpack');
      var path = require('path');
      var libraryName = 'TgeArmory';
      var outputFile = libraryName + '.js';

      var env = process.env.NODE_ENV;
      var mode = env;

      if (env === 'development') {
        outputFile = libraryName + '.js';
      } else if (env === 'production'){
        outputFile = libraryName + '.min.js';
      }

      var config = {
        mode: mode,
        entry: __dirname + '/src/main.js',
        devtool: 'source-map',
        output: {
          path: __dirname + '/public',
          filename: outputFile,
          library: libraryName,
          libraryTarget: 'umd',
          umdNamedDefine: true
        }
        // module: { ... },
        // resolve: { ... },
        // plugins: plugins
      }

      module.exports = config;
    </pre>
  </li>
  <li>
    Using the scripts we added in <b><i>package.json</i></b>, we can bundle JS files by running:
    <pre style="background: #eee">npm run opt</pre>
    to create compressed version, or use:
    <pre style="background: #eee">npm run dev</pre>
    to create uncompressed version.
  </li>
</ol>
