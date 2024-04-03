This is a [Next.js](https://nextjs.org/) project bootstrapped with [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.tsx`. The page auto-updates as you edit the file.

This project uses [`next/font`](https://nextjs.org/docs/basic-features/font-optimization) to automatically optimize and load Inter, a custom Google Font.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js/) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/deployment) for more details.

## Setting up the Project (found in *the docs*, why not here? Good question.)
## Create the app directory

For new applications, we recommend using the App Router. This router allows you to use React's latest features and is an evolution of the Pages Router based on community feedback.

Create an app/ folder, then add a layout.tsx and page.tsx file. These will be rendered when the user visits the root of your application (/).

### Populate files
**layout.tsx**
```
export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  )
}
```

**page.tsx**
```
export default function Page() {
  return <h1>Hello, Next.js!</h1>
}
```

**The public folder (optional)**

Create a public folder to store static assets such as images, fonts, etc. Files inside public directory can then be referenced by your code starting from the base URL (/).


# The app Router

In version 13, Next.js introduced a new App Router built on React Server Components, which supports shared layouts, nested routing, loading states, error handling, and more.

The App Router works in a new directory named app. The app directory works alongside the pages directory to allow for incremental adoption. This allows you to opt some routes of your application into the new behavior while keeping other routes in the pages directory for previous behavior. If your application uses the pages directory, please also see the Pages Router documentation.

- Good to know: The App Router takes priority over the Pages Router. Routes across directories should not resolve to the same URL path and will cause a build-time error to prevent a conflict.

By default, components inside app are React Server Components. This is a performance optimization and allows you to easily adopt them, and you can also use Client Components.

## Server & Client Components

### Server Components
React Server Components allow you to write UI that can be rendered and optionally cached on the server. In Next.js, the rendering work is further split by route segments to enable streaming and partial rendering, and there are three different server rendering strategies:

- Static Rendering
- Dynamic Rendering
- Streaming

[Server Components](https://nextjs.org/docs/app/building-your-application/rendering/server-components)

### Client Components

Client Components allow you to write interactive UI that is prerendered on the server and can use client JavaScript to run in the browser.
To use Client Components, you can add the React "use client" directive at the top of a file, above your imports.
`"use client"` is used to declare a boundary between a Server and Client Component modules. This means that by defining a "use client" in a file, all other modules imported into it, including child components, are considered part of the client bundle.

[Client Components](https://nextjs.org/docs/app/building-your-application/rendering/client-components)

# Routing

[Project Organization](https://nextjs.org/docs/app/building-your-application/routing/colocation)

## Roles of Folders and Files

Next.js uses a file-system based router where:

_Folders_ are used to define routes. A route is a single path of nested folders, following the file-system hierarchy from the root folder down to a final leaf folder that includes a page.js file. See Defining Routes.

_Files_ are used to create UI that is shown for a route segment. See special files.


## Nested Routes

To create a nested route, you can nest folders inside each other. For example, you can add a new /dashboard/settings route by nesting two new folders in the app directory.

The /dashboard/settings route is composed of three segments:

- / (Root segment)
- dashboard (Segment)
- settings (Leaf segment)

## File Conventions

Next.js provides a set of special files to create UI with specific behavior in nested routes:
	
- layout		Shared UI for a segment and its children
- page		Unique UI of a route and make routes publicly accessible
- loading		Loading UI for a segment and its children
- not-found		Not found UI for a segment and its children
- error	Error	 UI for a segment and its children
- global-error		Global Error UI
- route		Server-side API endpoint
- template		Specialized re-rendered Layout UI
- default		Fallback UI for Parallel Routes

Good to know: .js, .jsx, or .tsx file extensions can be used for special files.

## Component Hierarchy

The React components defined in special files of a route segment are rendered in a specific hierarchy:

-    layout.js
-    template.js
-    error.js (React error boundary)
-    loading.js (React suspense boundary)
-    not-found.js (React error boundary)
-    page.js or nested layout.js

## Safe colocation by default

In the app directory, nested folder hierarchy defines route structure.

Each folder represents a route segment that is mapped to a corresponding segment in a URL path.

However, even though route structure is defined through folders, a route is not publicly accessible until a page.js or route.js file is added to a route segment.

And, even when a route is made publicly accessible, only the content returned by page.js or route.js is sent to the client.

This means that project files can be safely colocated inside route segments in the app directory without accidentally being routable.



_Good to know_:

This is different from the _pages directory_, where any file in pages is considered a route.
While you can colocate your project files in app you don't have to. If you prefer, you can keep them outside the app directory.

### Private Folders

Private folders can be created by prefixing a folder with an underscore: _folderName

This indicates the folder is a private implementation detail and should not be considered by the routing system, thereby opting the folder and all its subfolders out of routing.

### Route Groups

Route groups can be created by wrapping a folder in parenthesis: (folderName)

This indicates the folder is for organizational purposes and should not be included in the route's URL path.

### src Directory

Next.js supports storing application code (including app) inside an optional src directory. This separates application code from project configuration files which mostly live in the root of a project.

### Module Path Aliases

Next.js supports Module Path Aliases which make it easier to read and maintain imports across deeply nested project files.

Example:
```
// before
import { Button } from '../../../components/button'
 
// after
import { Button } from '@/components/button'
```

# Project organization strategies

There is no "right" or "wrong" way when it comes to organizing your own files and folders in a Next.js project.

The following section lists a very high-level overview of common strategies. The simplest takeaway is to choose a strategy that works for you and your team and be consistent across the project.

Good to know: In our examples below, we're using components and lib folders as generalized placeholders, their naming has no special framework significance and your projects might use other folders like ui, utils, hooks, styles, etc.

## Store project files outside of app

This strategy stores all application code in shared folders in the root of your project and keeps the app directory purely for routing purposes.

## Store project files in top-level folders inside of app

This strategy stores all application code in shared folders in the root of the app directory.

## Split project files by feature or route

This strategy stores globally shared application code in the root app directory and splits more specific application code into the route segments that use them.

# Defining Routes

## Creating Routes
Next.js uses a file-system based router where folders are used to define routes.

Each folder represents a route segment that maps to a URL segment. To create a nested route, you can nest folders inside each other.

A special _page.js_ file is used to make route segments publicly accessible.

## Creating UI

Special file conventions are used to create UI for each route segment. The most common are pages to show UI unique to a route, and layouts to show UI that is shared across multiple routes.

For example, to create your first page, add a _page.js_ (could also be _page.tsx_ for Typescript?) file inside the app directory and export a React component:

Example:
```
export default function Page() {
  return <h1>Hello, Next.js!</h1>
}
```
[Defining Routes](https://nextjs.org/docs/app/building-your-application/routing/defining-routes)

## Pages and Layouts

The special files layout.js, page.js, and template.js allow you to create UI for a route. This page will guide you through how and when to use these special files.

### Pages

A page is UI that is unique to a route. You can define a page by default exporting a component from a page.js file.

For example, to create your index page, add the page.js file inside the app directory.
Then, to create further pages, create a new folder and add the page.js file inside it. For example, to create a page for the /dashboard route, create a new folder called dashboard, and add the page.js file inside it:

```
app -> /
app/page.js
app/dashboard/page.js -> /dashboard
```

_Good to know_:

- The .js, .jsx, or .tsx file extensions can be used for Pages.
- A page is always the leaf of the route subtree.
- A page.js file is required to make a route segment publicly accessible.
- Pages are Server Components by default, but can be set to a Client Component.
- Pages can fetch data. View the Data Fetching section for more information.

### Layouts & Templates

**Layouts** _preserve_ `State` and get somewhat involved; they require sharing _props_.
Check this out for info: [Layouts](https://nextjs.org/docs/app/building-your-application/routing/pages-and-layouts#layouts)

**Templates** are simliar but DOM elements are recreated, State is _not preserved_, effects are re-synchonized.

[Templates](https://nextjs.org/docs/app/building-your-application/routing/pages-and-layouts#templates)
[Pages and Layouts](https://nextjs.org/docs/app/building-your-application/routing/pages-and-layouts)
