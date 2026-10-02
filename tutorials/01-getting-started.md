# Getting started

Understand Chakra UI, prepare a React project, install the package, and render your first components.

[Back to tutorial index](../README.md)

---

## 1. What Chakra UI is

Chakra UI is a React component system for building web interfaces. It gives you composable components, style props, responsive values, and a theming system. Instead of writing a class for every small layout or spacing change, you can express many styles directly on a component.

See [Code example 1](#code-example-1) in the code section below.

Chakra UI is a UI layer, not a replacement for React, routing, data fetching, or application architecture. Use it alongside the tools your app already needs.

## 2. Before you start

You should be comfortable with:

- JavaScript fundamentals and JSX
- React components and props
- Basic HTML semantics
- npm or another Node package manager

The current Chakra UI setup requires **Node.js 20.x or newer**. This guide follows v3, so check your installed major version before copying examples from older tutorials.

## 3. Install and connect Chakra UI

### Install the packages

In an existing React project, install Chakra UI and its Emotion styling dependency:

See [Code example 2](#code-example-2) in the code section below.

### Add the provider

Wrap the application once near its root. The provider makes Chakra's styling system available to components below it.

See [Code example 3](#code-example-3) in the code section below.

If your project already has a provider, add ChakraProvider inside the existing root setup instead of creating a second React root. The official framework guide includes the Vite-specific setup and optional path aliases.

**Official guide:** [Install Chakra UI](https://chakra-ui.com/docs/get-started/installation) · [Use Chakra UI with Vite](https://chakra-ui.com/docs/get-started/frameworks/vite)

## 4. Build your first interface

Import the components you need and compose them like regular React components. Chakra components accept normal React props as well as Chakra style props.

See [Code example 4](#code-example-4) in the code section below.

Useful habits:

- Prefer Chakra components when they improve semantics or styling consistency.
- Use native elements when they are the clearest choice. Chakra's `as` prop can change the rendered element when appropriate.
- Give controls accessible names and visible focus styles.
- Keep application state and business logic in React, and keep design decisions in reusable components or theme configuration.


## All code samples in this chapter

### Code example 1

*Topic: 1. What Chakra UI is*

```jsx
import { Button } from "@chakra-ui/react"

export function SaveButton() {
  return <Button colorPalette="teal">Save changes</Button>
}
```

### Code example 2

*Topic: Install the packages*

```bash
npm install @chakra-ui/react @emotion/react
```

### Code example 3

*Topic: Add the provider*

```jsx
import React from "react"
import ReactDOM from "react-dom/client"
import { ChakraProvider, defaultSystem } from "@chakra-ui/react"
import App from "./App"

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <ChakraProvider value={defaultSystem}>
      <App />
    </ChakraProvider>
  </React.StrictMode>,
)
```

### Code example 4

*Topic: 4. Build your first interface*

```jsx
import { Button, Heading, Stack, Text } from "@chakra-ui/react"

export function WelcomePanel() {
  return (
    <Stack gap="4" align="start">
      <Heading size="lg">Welcome back</Heading>
      <Text color="fg.muted">Your workspace is ready.</Text>
      <Button colorPalette="blue">Open workspace</Button>
    </Stack>
  )
}
```

|  | [Next: Styling and layout →](02-styling-and-layout.md) |
|:--|--:|
