![Plugin banner](https://repository-images.githubusercontent.com/290913731/f64c9000-22e5-11eb-823a-85da58853d63)
Persist the Nuxt cache between Netlify builds for huge build speed improvements! ⚡️
[**One-click install to add this to your Nuxt site**](http://app.netlify.com/plugins/netlify-plugin-cache-nuxt/install?utm_source=github&utm_medium=nuxt-cache-bp-jl&utm_campaign=devex)</div>

## Usage

If you don’t want to use the [UI-based installation](http://app.netlify.com/plugins/netlify-plugin-cache-nuxt/install?utm_source=github&utm_medium=nuxt-cache-bp-jl&utm_campaign=devex), you can install manually using `netlify.toml`.

Add the following lines to your `netlify.toml` file:

```toml
[build]
  publish = "public"

[[plugins]]
  package = "netlify-plugin-cache-nuxt"
```

Note: The `[[plugins]]` line is required for each plugin, even if you have other plugins in your `netlify.toml` file already.

This plugin determines the location of your `.cache` folder by looking at the `publish` folder configured for Netlify deployment (this _must_ be set in your `netlify.toml` in the `[build]` section). This means that if your Nuxt site successfully deploys, it will be cached as well with no config required! 🎉

## How much of a difference does this plugin make in build times?

Each Nuxt site is different, so build times vary widely between them, but one common slowdown in Nuxt builds is processing and transforming images. Nuxt is smart enough to check if these transformations have already been done and skip them, but in order to get that benefit in a build pipeline (e.g. Netlify) the `public` and `.cache` directories need to be preserved between builds. That’s what this plugin does!

### Note: To be determined, don't look at the stats, don't
|                                                            | No Cache                                                                                                | Cache                                                                                                   | Savings |
|------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|---------|
| * 231 GraphQL queries<br>* 1,871 images<br>* 224 pages     | 293207ms ([build log](https://app.netlify.com/sites/lengstorf/deploys/5dceed27d58a580008daaccc))        | 72835ms ([build log](https://app.netlify.com/sites/lengstorf/deploys/5dcef2463da4810008d48aaa))         | 75%     |
| * 5 GraphQL queries<br>* No image processing<br>* 32 pages | 22072ms ([build log](https://app.netlify.com/sites/build-plugin-test/deploys/5dceed49e746a200091c76fe)) | 15543ms ([build log](https://app.netlify.com/sites/build-plugin-test/deploys/5dceedbfad95d0000bcd46d1)) | 30%     |

tl;dr: Repeat builds with lots of images will be _much_ faster. With few or no images, the difference will be there, but it won’t be as pronounced.

## Want to learn how to create your own Netlify Build Plugins?

Check out [Sarah Drasner’s excellent tutorial](https://www.netlify.com/blog/2019/10/16/creating-and-using-your-first-netlify-build-plugin/?utm_source=github&utm_medium=netlify-plugin-cache-nuxt-jl&utm_campaign=devex)!
