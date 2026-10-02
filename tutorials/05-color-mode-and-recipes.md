# Color mode and recipes

Set up dark mode, reuse component styles, and generate theme types with the CLI.

[Back to tutorial index](../README.md)

---

## 12. Add dark mode

Chakra UI v3 uses `next-themes` for color mode. The CLI generates a provider and color-mode helpers, including `useColorMode`; import those helpers from the generated snippet instead of importing them from `@chakra-ui/react` as older v2 examples do.

For theme-aware styles, prefer semantic tokens or conditions so colors adapt to the active mode. Keep the selected mode in the color-mode provider rather than manually toggling many component styles.

See [Code examples 1 and 2](#all-code-samples-in-this-chapter) for the setup commands and a toggle component.

**Official guide:** [Color mode](https://chakra-ui.com/docs/components/concepts/color-mode)

## 13. Reuse component styles with recipes

When multiple buttons or badges share a visual language, recipes let you centralize variants and sizes in the theme instead of repeating styling decisions.

See [Code example 3](#code-example-3) in the code section below.

Use a recipe for one component's variants, and a slot recipe when styling a component made of multiple related parts. Define only the variants your product needs, then use them consistently.

**Official guides:** [Recipes](https://chakra-ui.com/docs/theming/recipes) · [Customize recipes](https://chakra-ui.com/docs/theming/customization/recipes) · [Slot recipes](https://chakra-ui.com/docs/theming/slot-recipes)

## 14. Use the Chakra CLI

The CLI can add reusable snippets and generate types from your theme configuration.

See [Code example 4](#code-example-4) in the code section below.

Review generated files before adapting them to your project. Snippets are starter code, so keep only the providers and components your app actually uses.

**Official guide:** [Chakra CLI](https://chakra-ui.com/docs/get-started/cli)


## All code samples in this chapter

### Code example 1

*Topic: 12. Add dark mode*

```bash
npm install next-themes
npm install -D @chakra-ui/cli
npx chakra snippet add
npx chakra snippet add color-mode
```

The first snippet command generates the app provider. Use that generated `Provider` at your application root, then use the color-mode snippet for the toggle shown below. Keep only one Chakra provider around the app.

### Code example 2

*Topic: 12. Add dark mode*

```jsx
import { HStack, Text } from "@chakra-ui/react"
import { Provider } from "@/components/ui/provider"
import { ColorModeButton } from "@/components/ui/color-mode"

function AppHeader() {
  return (
    <HStack as="header" justify="space-between" p="4">
      <Text fontWeight="semibold">My workspace</Text>
      <ColorModeButton />
    </HStack>
  )
}

export function Root() {
  return (
    <Provider>
      <AppHeader />
    </Provider>
  )
}
```

The generated imports use the `@` source alias from the Vite setup guide. If your project uses another folder layout, adjust the import paths. If your app already has the generated `Provider` at its root, render `AppHeader` inside it instead of adding a second provider.

### Code example 3

*Topic: 13. Reuse component styles with recipes*

```jsx
// action-button.jsx
"use client"

import { chakra, defineRecipe } from "@chakra-ui/react"

const actionButtonRecipe = defineRecipe({
  base: {
    borderRadius: "lg",
    fontWeight: "semibold",
    transition: "background 0.2s",
  },
  variants: {
    variant: {
      solid: {
        bg: "blue.600",
        color: "white",
        _hover: { bg: "blue.700" },
      },
      outline: {
        borderWidth: "1px",
        borderColor: "blue.600",
        color: "blue.700",
      },
    },
    size: {
      sm: { h: "9", px: "4", fontSize: "sm" },
      lg: { h: "11", px: "6", fontSize: "md" },
    },
  },
  defaultVariants: {
    variant: "solid",
    size: "sm",
  },
})

export const ActionButton = chakra("button", actionButtonRecipe)

export function RecipeDemo() {
  return (
    <ActionButton type="button" variant="solid" size="lg">
      Publish
    </ActionButton>
  )
}
```

### Code example 4

*Topic: 14. Use the Chakra CLI*

```bash
npx chakra snippet list
npx chakra snippet add color-mode
npx chakra typegen ./theme.js
```

| [← Previous: Components and forms](04-components-and-forms.md) | [Next: Migration and practice →](06-migration-and-practice.md) |
|:--|--:|
