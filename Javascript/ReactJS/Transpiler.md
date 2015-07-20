## Introduction:
While developing ***ReactJS***, we often use ***JSX*** to describe the view of a component. However, the problem is that most browser do not know about the JSX syntax and as a result, we need to use a javascript transpiler/compiler.

This writeup will show how to setup the transpiler/compiler for your ReactJS project by either using [***Gulp***](http://gulpjs.com/) or [***Webpack***](http://webpack.github.io/). 

## Babel Transpiler/Compiler:

A transpiler/compiler is a tool that will help you tranfer one kind of language into another language. 

There are many javascript compilers out there which serve different purpose. You can check out this [github wiki](https://github.com/jashkenas/coffeescript/wiki/list-of-languages-that-compile-to-JS) to have a better understanding about this. Among so many different kind of javascript compilers, [***Babel***](https://babeljs.io/) is the one we will going to introduce today. 

***Babel*** (formerly known ad 6to5 ) is a javascript compiler. Babel can help you tranform your [**ES2015** (emcascript 6)](https://babeljs.io/docs/learn-es2015/) into the ecmascript 5 compatiable code. Moreover, the one of the feature that Babel provide is the ***JSX*** support. 

There are many ways for you to use Babel to compiler your source code; however in this writeup I will only conver two of them. 
> If you want to know more about the build system that Babel support please refer to this url: https://babeljs.io/docs/setup/

- **GulpJS**: http://gulpjs.com/
- **Webpack**: http://webpack.github.io/

## Build System: Gulp:
If you prefer using **Gulp** as your build tool. Just follow the steps and everything should work as you expected. 

### Required Module:
The following list the modules that we need to use during the building process.

- **gulp**
- **gulp-babel**

```bash
npm install --save-dev gulp
npm install --save-dev gulp-babel
```

### Config gulpfile.js:
The next step is to config your Gulp config file, ***gulpfile.js***.

First create the ***gulpfile.js*** in your project root.

```bash
cd $project_root
touch gulpfile.js
```

Next config the gulpfile.js like below. 

```javascript
var gulp = require('gulp');
var babel = require('babel');


var js_source_folder = "your project source folder";
var js_dest_folder = "public/";
gulp.task("default", function() {
	return gulp.src(js_source_folder + "/**/*.js")
		.pipe(babel())
		.pipe(gulp.dest(js_dest_folder));
});
```

> change the ***js\_source\_older*** to the javascript source folder in your project. 
> And ***js\_dest\_folder*** to the folder you want the compiled javascript code to store.

### Config package.json
The final step is to config your package.json.

```json
...
"scripts": {
	"build": "gulp"
},
...
```

After the above configuration, everytime you modify your code type

```bash
npm run build
```

Gulp will help you compile the code in ***js\_source\_folder*** and store the compiled code into ***js\_dest\_folder***.

## Build System: Webpack:
***Webpack*** is another build tool which will help you bundle the javascript file that you import in your source code.


### Required Module:
The following list the modules that is required:

- **webpack**
- **bable-loader**

```bash
npm install -g webpack
npm install --save-dev bable-loader
```

### Config webpack.config.js
Now it's time for us to write the config file for webpack. 

```javascript
module.exports = {
	entry: "./app/app.js",
	output: {
		path: __dirname,
		filename: "bundle.js"
	},
	module: {
		loaders: {
			test: /\.jsx?$/,
			exclude: /(node_modules|bower_components)/,
			loader: 'babel',	
			
		}
	}
};
```

### Config package.json
The final step is to config **package.json** as gulp.

```json
...
"scripts": {
	"check": "webpack",
	...
},
...
```

--