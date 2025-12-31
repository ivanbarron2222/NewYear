# Vercel Web Analytics Setup Guide

This guide documents how Vercel Web Analytics has been implemented in this project, following the official Vercel Web Analytics setup documentation.

## Overview

Vercel Web Analytics is already enabled and configured in this plain HTML project. This guide provides information on how the analytics tracking is set up and how to verify it's working correctly.

## Prerequisites for Implementation

To use Vercel Web Analytics, you need:

- A Vercel account ([sign up for free](https://vercel.com/signup))
- A Vercel project ([create a new project](https://vercel.com/new))
- The Vercel CLI installed (optional, but recommended)

Install the Vercel CLI:
```bash
npm install -g vercel
# or
yarn global add vercel
# or
pnpm add -g vercel
# or
bun add -g vercel
```

## Enabling Web Analytics in Vercel Dashboard

1. Go to your [Vercel dashboard](/dashboard)
2. Select your Project
3. Click the **Analytics** tab
4. Click **Enable** from the dialog

> **💡 Note:** Enabling Web Analytics will add new routes (scoped at `/_vercel/insights/*`) after your next deployment.

## Implementation for Plain HTML Sites

This project uses the plain HTML implementation of Vercel Web Analytics. 

### Setup in This Project

The following code has been added to `index.html` in the `<head>` section:

```html
<!-- Vercel Analytics -->
<script>
  window.va = window.va || function () { (window.vaq = window.vaq || []).push(arguments); };
</script>
<script defer src="/_vercel/insights/script.js"></script>
```

This implementation:
- Defines a `window.va` function to queue analytics events
- Loads the Vercel insights tracking script asynchronously using the `defer` attribute
- Works without requiring any additional npm packages

### Important Notes

- **No Route Support:** When using the plain HTML implementation, there is no automatic route tracking support. Only page views are tracked.
- **No Package Required:** Unlike other frameworks, the plain HTML implementation does not require the `@vercel/analytics` package.
- **Browser Network Tab:** Once deployed, you should be able to see a Fetch/XHR request in your browser's Network tab from `/_vercel/insights/view` when you visit any page.

## Deployment

To see analytics data, the project must be deployed to Vercel:

```bash
vercel deploy
```

Alternatively, if your Git repository is connected to Vercel, it will automatically deploy when you push commits to your main branch.

### After Deployment

Once your app is deployed:
1. Users visiting your site will be tracked
2. Page views and visitor data will be collected
3. You can view this data in your Vercel dashboard's Analytics tab

After a few days of visitor traffic, you'll be able to explore your data by viewing and filtering the analytics panels.

## Viewing Analytics Data

To view your Web Analytics data:

1. Go to your [Vercel dashboard](/dashboard)
2. Select your project
3. Click the **Analytics** tab
4. Explore your data and apply filters as needed

> **💡 Note:** Users on Pro and Enterprise plans can also add custom events to track user interactions such as button clicks, form submissions, or purchases.

## Verification Checklist

After deploying, verify that analytics is working:

- [ ] Vercel Web Analytics is enabled in your project dashboard
- [ ] `index.html` contains the `window.va` function definition
- [ ] `index.html` contains the script tag linking to `/_vercel/insights/script.js`
- [ ] The site is deployed to Vercel
- [ ] You can see the analytics fetch request in your browser's Network tab (in DevTools)
- [ ] Analytics dashboard shows visitor and page view data

## Additional Resources

For more information about Vercel Web Analytics, see:

- [Vercel Analytics Package Documentation](/docs/analytics/package)
- [Custom Events Guide](/docs/analytics/custom-events)
- [Data Filtering Guide](/docs/analytics/filtering)
- [Privacy and Compliance](/docs/analytics/privacy-policy)
- [Pricing and Limits](/docs/analytics/limits-and-pricing)
- [Troubleshooting Guide](/docs/analytics/troubleshooting)

## Framework-Specific Implementations

If you ever need to implement this in other frameworks, here's a quick reference:

### Next.js (Pages Directory)
Use the `Analytics` component from `@vercel/analytics/next` in `pages/_app.tsx`

### Next.js (App Directory)
Use the `Analytics` component from `@vercel/analytics/next` in `app/layout.tsx`

### React / Create React App
Use the `Analytics` component from `@vercel/analytics/react` in your main `App.tsx`

### Vue.js
Use the `Analytics` component from `@vercel/analytics/vue` in `src/App.vue`

### Svelte / SvelteKit
Use the `injectAnalytics` function from `@vercel/analytics/sveltekit` in `src/routes/+layout.ts`

### Astro
Use the `Analytics` component from `@vercel/analytics/astro` in your layout file

### Remix
Use the `Analytics` component from `@vercel/analytics/remix` in `app/root.tsx`

### Nuxt
Use the `Analytics` component from `@vercel/analytics/nuxt` in `app.vue`

### Plain HTML (This Project)
Include the `window.va` function and the analytics script in your HTML file (as implemented here).
