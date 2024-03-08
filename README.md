# Nuxt 3 Minimal Starter

Look at the [Nuxt 3 documentation](https://nuxt.com/docs/getting-started/introduction) to learn more.

## Setup

Make sure to install the dependencies:

```bash
# npm
npm install

# pnpm
pnpm install

# yarn
yarn install

# bun
bun install
```

## Development Server

Start the development server on `http://localhost:3000`:

```bash
# npm
npm run dev

# pnpm
pnpm run dev

# yarn
yarn dev

# bun
bun run dev
```

## Sync

Make nuxt and Capacitor sync

```bash
yarn sync
```

## Open Android app

Open app in Android Studio, to run it

```bash
yarn open:android
```

## Run Android app

Run the app in a Connected Android Device/Emulator

```bash
yarn android
```

## Android in Development

Open android in Development mode

Add the lines below to run the application in Development

```json
{
  "appId": "dev.patogordo.nuxt3",
  "appName": "nuxt3-android",
  "webDir": "dist",
  "bundledWebRuntime": false,
  "server": {
    "url": "http://192.168.1.15:3000",
    "cleartext": true
  }
}
```

Also run the nuxt development server with the command below

```bash
yarn dev
```
