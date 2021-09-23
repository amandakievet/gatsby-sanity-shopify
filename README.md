# Unopinionated Starter kit for [Gatsby](https://www.gatsbyjs.org/), [Sanity.io](https://www.sanity.io), & Shopify

BIG thanks to 🍝[Kevin Green](https://github.com/iamkevingreen)🍝 for the serverless function.

Clone this repository to bootstrap a fresh Gatsby site, powered by Sanity CMS and dynamically import Shopify products to Sanity with the help of a Web Hook.

_Note:_ This repo is **purposely** barebones so that you can employ your favorite CSS framework, create your sanity schemas, etc. For a more 'out of the box' starter, check out [Midway](https://github.com/ctrl-alt-del-world/midway) by [Kevin Green](https://github.com/iamkevingreen) or [HULL](https://github.com/ndimatteo/HULL) which is a great Next/Sanity/Shopify starter.

## Basic Instructions

### Initial Setup

1. Remove remote repo by entering `rm -rf .git`
2. Either create a new repo in this folder and version control both Sanity & Gatsby, or set up new repos for both folders

### Studio/

1. In the `studio` folder run `sanity init` and create a new project.
2. Update `studio/sanity.json` and update the Project ID.
3. Update the studio name in `studio/package.json`.
4. Edit schemas, add different content types, find out more here: [Sanity Docs](https://www.sanity.io/docs/sanity-studio)
5. Include these schemas in the `deskStructure.js` export (include a fun icon!)
6. Create a `READ/WRITE` API token. You'll need this for the Netlify serverless function.

### Web/

1. Rename `env.example` to `.env` by typing `mv env.example .env` in your terminal.
2. Enter your Sanity API keys in the `.env` file.
3. Modify `gatsby-config.js` and add your site title, etc.
4. Develop your front end, etc. (purposely left this ultra stripped-down)
5. Create a repo specifically for your Gatsby build, host with Netlify or anywhere you can have a Lambda function.

### Shopify

1. In your Netlify environment, go to your project and create a new Function.
2. Set the functions directory to be the `functions/` folder in your project.
3. In Shopify, go to `Settings -> Notifications -> Webhooks` and create webhooks for Product Creation, Updates, & Deletions (⚠️ Be careful with how you implement this, see more [here](https://github.com/lucasvocos/gatsby-sanity-shopify/blob/d69ed053dfa3e21b17a1c10e1b5697044774f70d/web/functions/shopify.js#L171)). Set the webhook's Callback URL to `[https://YOUR_URL.DOMAIN/.netlify/functions/shopify]` (if using Netlify, otherwise point to your provider's Lambda location)

## Features

**A blank slate Gatsby site w custom webhook to create new Shopify products**

- 📡 Real-time content preview in development
- ⏱ Fast & frugal builds
- 🗃 No accidental missing fields/types
- 🧰 Full Render Control with Portable Text
- 📸 gatsby-image support
- 🔧 Minimal configuration
- 💻 Custom serverless function that will create/update products from Shopify, as well as flag deleted items
- 🚧 Jest testing suite support

**Sanity Studio with a schema for**

- 🏢 Site settings
- 📃 Pages
- 📰 Posts
- 🛍 Products & Variants
  - Products have default settings for `title`, `slug`, `defaultPrice`, `id`, `productId`.
  - Variants have default settings for `id`, `productId`, `variantId`, `title`, `variantTitle`, `sku`, and `price`.
  - The `web/functions/shopify` file will generate new Sanity documents with these default fields.
  - To add/remove fields please refer to the sample API response here: https://shopify.dev/docs/admin-api/rest/reference/events/webhook#list-of-supported-webhook-events-and-topics-2021-01

## Credits

This entire repo is really just merged together from a stripped-down version of Sanity's [Sample company website built with Gatsby & Sanity.io](https://github.com/sanity-io/example-company-website-gatsby-sanity-combo) repo and a modified version of [Kevin Green](https://github.com/iamkevingreen)'s lambda function as discussed in the [Sanity + Shopify Roundtable: Headless ecommerce with Kevin Green & Joseph Thomas](https://www.youtube.com/watch?v=4mgI333aGvo) video.

## License

MIT
