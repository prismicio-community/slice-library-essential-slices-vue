# slice-library-essential-slices-vue

A nicely made Slice Library for [Nuxt.js][nuxtjs].

## Demo

<a href="#"><img src="https://angeloashmore-slicemachine-intro.cdn.prismic.io/angeloashmore-slicemachine-intro/49ca4bde-b36a-42f4-a072-60d2e5202f85_try-button.svg" alt="Try on Slice Showcase" width="200" /></a>

## Quick Start

Start a new [Slice Machine][slicemachine] project with this Slice Library with the following command:

```bash
npx @slicemachine/init@latest --lib prismicio-community/slice-library-essential-slices-vue
```

The same command can be used to add the Slice Library to an existing Slice Machine project.

## Post-Install Setup

Declare `reset.css` and `styles.css` in `nuxt.config.js` CSS resources:

```js
export default {
	/* ... */

	css: ["~~/essential-slices/reset.css", "~~/essential-slices/styles.css"],
};
```

[nuxtjs]: https://nuxtjs.org
[slicemachine]: https://slicemachine.dev
