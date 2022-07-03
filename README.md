# How to run [Next.js](https://nextjs.org/) with [TailwindCSS](https://tailwindcss.com/), [Prettier](https://prettier.io/), [ESLint](https://eslint.org/), and [TypeScript](https://www.typescriptlang.org/)

## Useful VSCode extensions:

- ESLint
- Prettier
- Tailwind CSS IntelliSense

# How to install all of this

```powershell
yarn create next-app --typescript
```

I am not sure if the following is needed.

```powershell
yarn lint
```

Add all the packages and plugins in one go.

```powershell
yarn add -D @typescript-eslint/eslint-plugin prettier eslint-config-prettier tailwindcss postcss autoprefixer prettier-plugin-tailwindcss eslint-plugin-tailwindcss
```

```powershell
yarn run tailwindcss init -p
```

Add content to tailwind.config.js

```json
{
  "content": [
    "./pages/**/*.{js,ts,jsx,tsx}",
    "./components/**/*.{js,ts,jsx,tsx}"
  ]
}
```

Add plugins, extends entries, and rules to '.eslintrc.json'.
Before:

```json
{
  "extends": "next/core-web-vitals"
}
```

After:

```json
{
  "plugins": ["@typescript-eslint", "tailwindcss"],
  "extends": [
    "next/core-web-vitals",
    "plugin:@typescript-eslint/recommended",
    "plugin:tailwindcss/recommended",
    "prettier"
  ],
  "rules": {
    "prefer-const": "error",
    "@typescript-eslint/no-unused-vars": "error",
    "@typescript-eslint/no-explicit-any": "error"
  }
}
```

Create '.prettierrc.json' with the following content:

```json
{
  "semi": true,
  "trailingComma": "all",
  "singleQuote": true,
  "tabWidth": 2,
  "useTabs": false
}
```

Create prettier.config.js with the following content:
Saving this will take a long time.

```javascript
module.exports = {
  pllugins: [require('prettier-plugin-tailwindcss')],
};
```

Next, go to styles/global.css and add the following at the beginning of the file:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Add the following to VSCode's settings.json.

[TailwindCSS Extension](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss)

```json
{
  "editor.quickSuggestions": {
    "other": true,
    "comments": true,
    "strings": true // This is recommended by the TailwindCSS VSCode Extension to enable a better experience.
  },
  "files.associations": {
    "*.css": "tailwindcss" // This is necessary to remove the unknown warnings in 'global.css'.
  },
  "[json]": {
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "esbenp.prettier-vscode" // This lets prettier handle the formatting for these filetypes.
  },
  "[javascript]": {
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescript]": {
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascriptreact]": {
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "esbenp.prettier-vscode" // JSX
  },
  "[typescriptreact]": {
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "esbenp.prettier-vscode" // TSX
  }
  ...
}
```

Finally, run

```powershell
yarn dev
```

and it should work like a charm!

## tests

Add test.ts and add the following:

```typescript
export let VERSION = '1.0.0';
```

On save it should turn into:

```typescript
export const VERSION = '1.0.0';
```

Chnange the h1 in 'index.tsx' to:

```JSX
<h1 className="text-6xl text-blue-900 underline mx-5 my-5">
          Welcome to <a href="https://nextjs.org">Next.js!</a>
</h1>
```

It should change to:

```JSX
<h1 className="m-5 text-6xl text-blue-900 underline">
          Welcome to <a href="https://nextjs.org">Next.js!</a>
</h1>
```

# Here starts the standard [Next.js](https://nextjs.org/) readme.

This is a [Next.js](https://nextjs.org/) project bootstrapped with [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `pages/index.tsx`. The page auto-updates as you edit the file.

[API routes](https://nextjs.org/docs/api-routes/introduction) can be accessed on [http://localhost:3000/api/hello](http://localhost:3000/api/hello). This endpoint can be edited in `pages/api/hello.ts`.

The `pages/api` directory is mapped to `/api/*`. Files in this directory are treated as [API routes](https://nextjs.org/docs/api-routes/introduction) instead of React pages.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js/) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/deployment) for more details.
