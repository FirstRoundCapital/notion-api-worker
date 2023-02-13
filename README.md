![Notion API Worker](https://user-images.githubusercontent.com/1440854/79893752-cc448680-8404-11ea-8d19-e0308eb32028.png)
![API Version](https://badgen.net/badge/API%20Version/v1/green)

THIS IS A FORK OF [THIS OPEN SOURCE REPOSITORY](https://github.com/splitbee/notion-api-worker)

To run with wrangler locally, specify the entrypoint with wrangler:

`wrangler dev worker/script.js`

[Wrangler docs](https://developers.cloudflare.com/workers/wrangler/)

A **serverless wrapper** for the private Notion API. It provides fast and easy access to your Notion content.
Ideal to make Notion your CMS.

This project is self-hosted at firstround.cloud on [Cloudflare](https://dash.cloudflare.com/).

_Use with caution. This is based on the private Notion API. We can not gurantee it will stay stable._

## Features

🍭 **Easy to use** – Receive Notion data with a single GET request

🗄 **Table Access** – Get structured data from tables & databases

✨ **Blazing Fast** – Built-in [SWR](https://www.google.com/search?q=stale+while+revalidate) caching for instant results

🛫 **CORS Friendly** – Access your data where you need it

## Use Cases

- Use it as data-source for blogs and documentation. Create a table with pages and additional metadata. Query the `/table` endpoints everytime you want to render a list of all pages.

- Get data of specific pages, which can be rendered with [`react-notion`](https://github.com/splitbee/react-notion)

## Endpoints

### Load page data

`/v1/page/<PAGE_ID>`

Example ([Source Notion Page](https://www.notion.so/react-notion-example-2e22de6b770e4166be301490f6ffd420))

[`https://firstround.cloud/v1/page/2e22de6b770e4166be301490f6ffd420`](https://firstround.cloud/v1/page/2e22de6b770e4166be301490f6ffd420)

Locally:
[`http://172.20.2.14:8787/v1/page/2e22de6b770e4166be301490f6ffd420`](http://172.20.2.14:8787/v1/page/2e22de6b770e4166be301490f6ffd420)


Returns all block data for a given page.
For example, you can render this data with [`react-notion`](https://github.com/splitbee/react-notion).

### Load data from table

`/v1/table/<PAGE_ID>`

Example ([Source Notion Page](https://firstround.cloud/20720198ca7a4e1b92af0a007d3b45a4?v=4206debfc84541d7b4503ebc838fdf1e))

[`https://firstround.cloud/v1/table/20720198ca7a4e1b92af0a007d3b45a4`](https://firstround.cloud/v1/table/20720198ca7a4e1b92af0a007d3b45a4)

Locally:
[`http://172.20.2.14:8787/v1/table/20720198ca7a4e1b92af0a007d3b45a4`](http://172.20.2.14:8787/v1/table/20720198ca7a4e1b92af0a007d3b45a4)

## Authentication for private pages

All public pages can be accessed without authorization. If you want to fetch private pages there are two options.

- The recommended way is to host your own worker with the `NOTION_TOKEN` environment variable set. You can find more information in the [Cloudflare Workers documentation](https://developers.cloudflare.com/workers/reference/apis/environment-variables/). This is what we currently do.

### Receiving the token

To obtain your token, login to Notion and open your DevTools and find your cookies. There should be a cookie called `token_v2`, which is used for the authorization.

### Deploys

Deploys are done using [wrangler](https://github.com/cloudflare/workers-sdk).
See the wrangler.example.toml file for configuration.

Install wrangler with `https://github.com/cloudflare/workers-sdk`.
Configure using `wrangler login`.

After configuring the .toml file, you can deploy with `wrangler publish worker/script.js`.

## Credits

- [Timo Lins](https://twitter.com/timolins) – Idea, Documentation
- [Tobias Lins](https://twitter.com/linstobias) – Code
- [Travis Fischer](https://twitter.com/transitive_bs) – Code
