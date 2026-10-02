# Theming

Use semantic colors and tokens, then create a custom Chakra system.

[Back to tutorial index](../README.md)

---

## 8. Use colors and design tokens

Tokens are named design values such as colors, spacing, and font sizes. Using tokens keeps the interface consistent and makes later redesigns easier.

See [Code example 1](#code-example-1) in the code section below.

Chakra includes semantic tokens for common roles, such as foreground and background. Prefer semantic values like `fg.muted` and `bg.panel` when the color's role matters more than its literal hue. Use a component's `colorPalette` when you want coordinated component colors:

See [Code example 2](#code-example-2) in the code section below.

**Official guides:** [Design tokens](https://chakra-ui.com/docs/theming/tokens) · [Colors](https://chakra-ui.com/docs/theming/colors) · [Semantic tokens](https://chakra-ui.com/docs/theming/semantic-tokens) · [CSS variables](https://chakra-ui.com/docs/styling/css-variables)

## 9. Customize the theme

In v3, configure a system with `defineConfig` and `createSystem`. Token values use an object with a `value` field.

See [Code example 3](#code-example-3) in the code section below.

Pass the custom system to the provider:

See [Code example 4](#code-example-4) in the code section below.

You can also define semantic tokens, breakpoints, recipes, and global styles in the system configuration. Keep shared values in the theme instead of repeating raw values across many components.

**Official guides:** [Theming overview](https://chakra-ui.com/docs/theming/overview) · [Design tokens](https://chakra-ui.com/docs/theming/tokens) · [Customize colors](https://chakra-ui.com/docs/theming/customization/colors)


## All code samples in this chapter

### Code example 1

*Topic: 8. Use colors and design tokens*

```jsx
import { Box, Text } from "@chakra-ui/react"

export function TokenPanel() {
  return (
    <Box bg="bg.panel" color="fg" borderColor="border" borderWidth="1px" p="4">
      <Text color="fg.muted">Secondary information</Text>
    </Box>
  )
}
```

### Code example 2

*Topic: 8. Use colors and design tokens*

```jsx
import { Button } from "@chakra-ui/react"

export function PaletteButton() {
  return <Button colorPalette="purple">Create project</Button>
}
```

### Code example 3

*Topic: 9. Customize the theme*

```jsx
// theme.js
import { createSystem, defaultConfig, defineConfig } from "@chakra-ui/react"

const config = defineConfig({
  theme: {
    tokens: {
      colors: {
        brand: {
          500: { value: "#6d5dfc" },
          600: { value: "#5947e8" },
        },
      },
    },
    semanticTokens: {
      colors: {
        surface: {
          card: { value: { base: "{colors.gray.50}", _dark: "{colors.gray.900}" } },
        },
        text: {
          muted: { value: { base: "{colors.gray.600}", _dark: "{colors.gray.300}" } },
        },
      },
    },
  },
})

export const system = createSystem(defaultConfig, config)
```

### Code example 4

*Topic: 9. Customize the theme*

```jsx
import { Box, ChakraProvider, Text } from "@chakra-ui/react"
import { system } from "./theme"

export function ThemePreview() {
  return (
    <ChakraProvider value={system}>
      <Box bg="surface.card" p="6" borderRadius="xl">
        <Text color="brand.500" fontWeight="bold">Branded heading</Text>
        <Text color="text.muted">This surface and text adapt to the color mode.</Text>
      </Box>
    </ChakraProvider>
  )
}
```

## All Q&A in this chapter

### 1. How are a design token and a semantic token different?

A design token names a concrete value, such as `brand.500`. A semantic token names a purpose, such as `text.muted` or `surface.card`, so its value can change by color mode while its meaning stays the same.

### 2. How do you add and use a brand color token?

Add a value such as `500: { value: "#6d5dfc" }` under `theme.tokens.colors.brand`, then use it with a style prop such as `<Text color="brand.500">Brand label</Text>`. The complete system setup is in Code examples 3 and 4.

### 3. When should you choose `fg.muted` or `bg.panel` over a literal color?

Use those semantic tokens when the color represents a role, such as secondary text or a panel surface. The theme can then keep that role readable across light and dark modes.

### 4. Why pass the custom system to ChakraProvider?

ChakraProvider supplies the system to the component tree. If you omit the custom system, components continue using the default system and cannot resolve your custom tokens.

### 5. How can a semantic color token adapt to light and dark mode?

Give the token a mode-aware value, for example `value: { base: "{colors.gray.600}", _dark: "{colors.gray.300}" }`. The token name stays the same while its resolved color changes with the active mode.

---

| [← Previous: Styling and layout](02-styling-and-layout.md) | [Next: Components and forms →](04-components-and-forms.md) |
|:--|--:|
