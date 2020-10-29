# Hydra Studios Shopify

## Getting Set Up for Local Development

### Set up ThemeKit

[ThemeKit](https://shopify.github.io/themekit) is the Shopify CLI that allows you to interact with themes through the command line.

To set it up, install through Homebrew

```shell
brew tap shopify/shopify
brew install themekit
```

### Set up Theme in Store

Go to the [themes page](https://hydra-studios-wall-street.myshopify.com/admin/themes), find the live theme, then click "Actions" and "Duplicate".  The duplication will take up to a minute. Once the new duplicate is completed, rename it to something like `myname-dev`

### Create Private app

Before creating a private app, the store owner must enable private apps for their store.

[Here's how](https://help.shopify.com/en/manual/apps/private-apps#enable-private-app-development-from-the-shopify-admin)

Once private apps are enabled, create one.  If Tanooki already has one, you should use that same one instead of creating a second private app.

### Download Theme for Local Development

First, get the private app's password at [the private app's page](PLACEHOLDER).

Then, get your theme's ID (replacing MY_APP_PASSWORD with the result from above):

```
theme get --list -p=MY_APP_PASSWORD -s=https://hydra-studios-wall-street.myshopify.com
```

This will get you a list of numbers in brackets followed by the theme name.  That number is your theme ID.

You can now use that theme ID to download the application for local development.  This step may take up to 10 minutes.

```
theme get -p=MY_APP_PASSWORD -s=MY_APP_NAME.myshopify.com --themeid=MY_THEME_ID
```

After the download, the command above will alse configure a local `config.yml` file which should look something like:
```yaml
development:
  password: MY_APP_PASSWORD
  theme_id: MY_THEME_ID
  store: hydra-studios-wall-street.myshopify.com
```

### Start a Watcher

In order to automatically update your theme whenever a change is made locally, you must start a watcher process.

To start watcher, run:
```
theme deploy -e=development
```

You can access the live preview in one of two ways
1. Go to https://hydra-studios-wall-street.myshopify.com/?preview_theme_id=MY_THEME_ID
2. Run `theme open -e=development`

If you see your changes, you're all set for local development!
