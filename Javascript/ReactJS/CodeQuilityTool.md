# Introduction:
One import thing while developing javascript is the static checker tools or code quility tools. It not only gives you some javascript syntax error, but also pointed out some potential problems in your source code. There are many code quility tools out there. for example:

- [**jslint**] (http://www.jslint.com/) 
- [**jshint**] (http://http://jshint.com/)
- [**eslint**] (http://eslint.org/)
- etc

There is no exact answer about which one is the best, there is only which one is more suitable for your current project. 

I recently start learning about **ReactJS** and playing with some React code. Everything is fine except that the code quility tool that I'm using cannot recognize the [**JSX syntax**](https://facebook.github.io/react/docs/jsx-in-depth.html). As a result, the tool keeps complain about the syntax error in my javascirpt files. 

After google for a while, I finally found out some useful tips to properly setup the checking tool when developing ReactJS. In this writup, I will walkthrough how to setup the checking environemnt for ReactJS/JSX.

# Npm Modules:
First of all, I have assume you have install nodejs in your developing system, so I will not talk about how to install node. The following are the modules that we need to setup the proper checking envirnment.

- [**eslint**](http://eslint.org)
- [**babel-eslint**](https://www.npmjs.com/package/babel-eslint)
- [**eslint-plugin-react**](https://www.npmjs.com/package/eslint-plugin-react)


Typing the following command to install the modules.

```bash
npm install -g eslint
npm install -g babel-eslint
npm install -g eslint-plugin-react

```


> ***Note***: 
> **Eslint** itself understands the **JSX syntax**. However, there are still other things that we want the checker to warn us. For example, the **propTypes** and **displayName** for a *React component*. And this is why I have installed **eslint-plugin-react** module. This module gives more eslint rules for us to configure while developing ReactJS.

# Eslint Config File:
Based on the official website, there are three way to let the eslint know which options you want to enable.

- *inline comment*
- *.eslintrc*
- *inside package.json*

In my case, I will use *.eslintrc* for example. The following is the example *.eslintrc* files.

```json
{
	"parser": "babel-eslint",
	"ecmaFeatures": {
		"modules": true,
		"jsx": true
	},
	"environment": {
		"browser": true,
	},
	"plugins": [
		"react"
	],
	"rules": {
		"react/display-name": 1,
		"react/prop-types": 1,
		"react/wrap-multilines": 2
	}
}
```
You can checkout the result by typing:

```bash
find app/ | grep js | xargs eslint
```

A simple walkthrough of the above config file:

- **parser**: eslint support using different javascript parser. The default one is espree. 
- **environment**: specifiy which environment you are currently developing, in our case, the browser environment.
- **plugins**: eslint support different plugins, in our case, we use the react plugins for more support.
- **rules**: specifiy the rules you prefer to use.

The official site has explains those fields in details. I strongly recommended you reading the documentation.

- **Configure Eslint**: http://eslint.org/docs/user-guide/configuring
- **Rules for Eslint**: http://eslint.org/docs/rules/
- **Rules for React Plugins**: https://github.com/yannickcr/eslint-plugin-react#list-of-supported-rules

# Setup package.json:
The last step is to add the checking command to **package.json** so that we don't need to type the previous command all the time. 

> Note that you can use other tools such as [**gulp-eslint**](https://github.com/adametry/gulp-eslint) or [**eslint-watch**](https://www.npmjs.com/package/eslint-watch) to accomplish the same goal. 

The following is a simple example that we add the bash command into the **package.json scripts** field.

```json
...
"scripts": {
	"check": "find app/ | grep js | xargs eslint",
	"test": "echo \"Error: no test sepecified\" && exit 1"
},
...
```

After that typing the following command should check all the javascript files inside app folder.

```bash
npm run check
```

