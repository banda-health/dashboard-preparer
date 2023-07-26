# dashboard-preparer
This code contains the necessary steps to compile React &amp; Tremor into bundled code that can be included in HTML to dynamically build components.

If any code needs to be updated, just update it from `npm` or `yarn` and redo the steps below.

## Pre-Compiling Code

### Building the React-Tremor-HeroIcons Bundle
We need all dependencies bundled into one JS file so we can leverage it after Babel compiles the code. The idea for this can be seen in this [video where JS dependencies are manually compiled](https://www.youtube.com/watch?v=UNMkLHzofQI).

To create the bundle:
1. From the command line, navigate to the folder `react-tremor-bundle`
```
cd react-tremor-bundle
```
2. Run the webpack builder:
```
npx webpack-cli ./src/index.js
```
3. Take the ouptput file `./react-tremor-bundle/node_modules/react-tremor-bundle.js` and use it as you need. The basic use will be something like:
```javascript
window.reactTremorBundle=((__magic__, exports, module) => {/*Bundled code*/});
```

#### Splitting out Components
If you allow users to enter their own components, you will need to map them to your compiled object (`window.reactTremorBundle` in the example above). To do this, you need to compile a list of all component names that exist in your bundle and have them in an available array, possible split out by library.

A good way to do this is to browse the original compiled code's packaging and get the file names. For example, for heroicons, you can do this via unpkg:
```
https://unpkg.com/browse/@heroicons/react/20/solid/
```
or by just looking in `./node_modules/@heroicons/react/20/solid`.

### Getting CSS for Tailwind & Tremor
Tremor relies on Tailwind CSS, so we need to generate the necessary Tailwind classes for Tremor to use.
1. Run `npm run build`.
2. Take the contents of `./dist/assets/index-[hash].css` and place it in a CSS file to reference from your app.
