# Smelte
[![license](https://img.shields.io/npm/l/smelte.svg)](https://img.shields.io/npm/l/smelte.svg)
[![downloads](https://img.shields.io/npm/dm/smelte.svg)](https://img.shields.io/npm/dm/smelte.svg)
[![version](https://img.shields.io/npm/v/smelte.svg)](https://img.shields.io/npm/v/smelte.svg)

[Demo](https://smelte.netlify.com/)

Smelte is a UI framework built on top of Svelte and Tailwind CSS using Material Design spec (hence the name).
It comes with many components and utility functions making it easy to build beautiful responsive layouts while keeping
bundle size and performance at check all thanks to Svelte.

### Installation
Clone the project's template, install the dependencies and write some pretty code!
```
npx degit matyunya/smelte-sapper-template my-svelte-project
cd my-svelte-project
yarn && yarn dev
(or npm install && npm run dev)
```

If you don't want to use sapper you can use raw template:

```
npx degit matyunya/smelte-template my-svelte-project
```

### Adding to existing project
First add the dependencies:
```
yarn add smelte tailwindcss rollup-plugin-postcss svelte-preprocess @fullhuman/postcss-purgecss postcss-import tailwindcss-elevation
```

Add following to `postcss.config.js` in your project's root directory
```
const production = !process.env.ROLLUP_WATCH;
const purgecss = require("@fullhuman/postcss-purgecss");

module.exports = {
  plugins: [
    require("postcss-import")(),
    require("tailwindcss")("./node_modules/smelte/tailwind.config.js"),
    require("autoprefixer"),
    production &&
      purgecss({
        content: ["./**/*.html", "./**/*.svelte"],
        defaultExtractor: content => content.match(/[A-Za-z0-9-_:/]+/g) || []
      })
  ]
};
```

Add postcss to your Rollup config:
```
import postcss from "rollup-plugin-postcss";
import autoPreprocess from "svelte-preprocess";

...

plugins: [
  svelte({
    preprocess: autoPreprocess({
      postcss: true
    }),
    // enable run-time checks when not in production
    dev: !production,
    // we'll extract any component CSS out into
    // a separate file — better for performance
    css: css => {
      css.write("public/bundle.css");
    }
  }),
  postcss({
    extract: "public/utils.css"
  }),
```

Add exported css file to `public/index.html`:
```
<link rel='stylesheet' href='/utils.css'>
```

Create `smelte.css` in `src` folder with this line:
```
@import 'smelte/src/tailwind';
```

And import it in your `src/main.js`:
```
import './tailwind.css';
```

That's it! The process is quite tedious at the moment. Please send feedback if you know how to make it better.

### Components
- [x] Text field
- [x] Button
- [x] Select
- [x] Checkbox
- [x] Radio
- [x] List
- [x] Chip
- [x] Menu
- [x] Navigation drawer
- [x] Snackbar
- [x] Dialog
- [x] Card
- [x] Slider
- [x] Proper customization via class props
- [x] Data table
- [x] Autocomplete
- [x] Tooltip
- [x] Revise events (on:change, on:focus, on:input...)
- [x] Treeview
- [ ] Form
- [ ] Date picker
- [ ] Stepper
- [ ] Upload
- [ ] Rating
- [ ] Pagination
- [ ] Breadcrumbs

### Features
- [x] Default typography per Material design spec
- [x] Material icons
- [x] CSS ripple animation
- [x] Image lazy loading
- [x] Now SSR deployment
- [x] Color palette generator
- [x] Improve Purge CSS
- [x] Theming
- [x] Image processing (done [here](https://github.com/matyunya/svelte-image))
- [x] Svelte template (without Sapper)
- [x] JS ripple animation
- [ ] Dark mode
- [ ] Other icons
- [ ] Document API
- [ ] IE 11 support