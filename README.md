![Nuxt LCP Speedup](./.github/og.jpg)

# Nuxt LCP Speedup

[![npm version](https://img.shields.io/npm/v/nuxt-lcp-speedup?color=a1b858&label=)](https://www.npmjs.com/package/nuxt-lcp-speedup)

[Nuxt](https://nuxt.com) module to optimize Largest Contentful Paint (LCP) for Lighthouse and Google PageSpeed Insights.

## Why?

Large Nuxt applications with dynamic imports and image assets can suffer from poor performance scores in Lighthouse and Google PageSpeed Insights. This module addresses the issue by disabling prefetching of dynamic imports and filtering image assets from the build manifest.

The module supports two prefetch strategies that hook into the Nuxt build process to optimize the LCP score: `none` and `prefetchStrategy`.

- `none`: Disables prefetching for all dynamic imports. As a result, all `<link rel="prefetch">` tags are removed from the HTML.
- `excludeImages`: Filter image assets from the build manifest. This prevents the browser from prefetching images, which can delay the rendering of the main content. Script and style assets will not be affected. You can define a custom list of image extensions to filter in the [module options](#module-options).

## Setup

```bash
npx nuxi@latest module add nuxt-lcp-speedup
```

## Usage

Add the Nuxt LCP Speedup to your Nuxt configuration and you're good to go:

```ts
// `nuxt.config.ts`
export default defineNuxtConfig({
  modules: ['nuxt-lcp-speedup']
})
```

To customize the module, configure the `lcpSpeedup` option in your Nuxt configuration:

```ts
// `nuxt.config.ts`
export default defineNuxtConfig({
  modules: ['nuxt-lcp-speedup'],

  lcpSpeedup: {
    prefetchStrategy: 'excludeImages'
  }
})
```

## Module Options

```ts
interface ModuleOptions {
  /**
   * Enable or disable the module.
   *
   * @default true
   */
  enabled?: boolean
  /**
   * Determines which assets to remove from the manifest.
   *
   * @default 'none'
   */
  prefetchStrategy?: 'none' | 'excludeImages'
  /**
   * List of image extensions to remove from the manifest.
   *
   * @default ['gif', 'jpg', 'jpeg', 'png', 'svg', 'webp']
   */
  imageExtensions?: string[]
}
```

## 💻 Development

1. Clone this repository
2. Enable [Corepack](https://github.com/nodejs/corepack) using `corepack enable`
3. Install dependencies using `pnpm install`
4. Run `pnpm run dev:prepare`
5. Start development server using `pnpm run dev`

## Credits

- All the discussions and contributions in the [Nuxt GitHub issue](https://github.com/nuxt/nuxt/issues/18376) that inspired this module.

## License

[MIT](./LICENSE) License © 2024-PRESENT [Johann Schopplich](https://github.com/johannschopplich)
