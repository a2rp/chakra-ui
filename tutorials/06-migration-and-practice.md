# Migration and practice

Review the v2 to v3 migration path, build a practice card, and troubleshoot common issues.

[Back to tutorial index](../README.md)

---

## 15. Move from Chakra UI v2 to v3

Do not assume v2 examples work unchanged in v3. The system setup, color mode, and many component APIs changed. For example, v3 uses `ChakraProvider value={system}`, and components such as Accordion use compound parts like `Accordion.Root` and `Accordion.Item`.

When upgrading:

1. Read the official migration guide before changing dependencies.
2. Update the provider and theme configuration.
3. Migrate component APIs one component at a time.
4. Replace old color-mode usage with the v3 `next-themes` setup if needed.
5. Run the app and verify keyboard behavior, responsive styles, and visual states.

Compare the provider syntax in Code examples 2 and 3 under [All code samples in this chapter](#all-code-samples-in-this-chapter). A common component prop change is `colorScheme` in v2 to `colorPalette` in v3.

**Official guide:** [Migration from v2 to v3](https://chakra-ui.com/docs/get-started/migration)

## 16. Practice project: profile card

Build this small card after finishing the lessons. It practices composition, spacing, semantic text colors, responsive width, and a clear action.

See [Code example 1](#code-example-1) in the code section below.

Try extending it: add a responsive stack of skills, make the action a real link, and add a second theme color palette. Check the current [Avatar](https://chakra-ui.com/docs/components/avatar) and [Badge](https://chakra-ui.com/docs/components/badge) docs if your installed version has different component parts.

## 17. Common problems

| Symptom | Check |
| --- | --- |
| Components render without Chakra styles | Confirm the app is wrapped in `ChakraProvider` and the right system is passed through `value`. |
| A copied tutorial has unknown props | Check whether the tutorial targets v2 or v3, then compare it with the current component docs. |
| Theme token changes do not appear | Confirm the custom system is the one passed to ChakraProvider and that token values use `{ value: ... }`. |
| Color mode hooks cannot be imported | Use the v3 color-mode setup based on `next-themes` and the official generated snippet. |
| A responsive value looks wrong | Confirm it is mobile-first and uses a supported breakpoint key. |
| TypeScript does not know custom tokens | Run the Chakra CLI type generator and include its generated types in the project. |


## All code samples in this chapter

### Code example 1

*Topic: 16. Practice project: profile card*

```jsx
import { Avatar, Badge, Box, HStack, Link, Stack, Text } from "@chakra-ui/react"

export function ProfileCard() {
  return (
    <Box
      w="full"
      maxW="sm"
      borderWidth="1px"
      borderColor="border"
      borderRadius="2xl"
      bg="bg.panel"
      p={{ base: "5", md: "6" }}
    >
      <Stack gap="5">
        <HStack align="center" gap="4">
          <Avatar.Root size="lg">
            <Avatar.Fallback name="Ashish Ranjan" />
          </Avatar.Root>
          <Stack gap="1">
            <Text fontWeight="bold">Ashish Ranjan</Text>
            <Text color="fg.muted" fontSize="sm">Full-stack developer</Text>
          </Stack>
        </HStack>
        <Text color="fg.muted">
          Building practical web applications and learning by shipping projects.
        </Text>
        <HStack wrap="wrap" gap="2">
          <Badge>React</Badge>
          <Badge>Node.js</Badge>
          <Badge>MongoDB</Badge>
        </HStack>
        <HStack justify="space-between" wrap="wrap" gap="3">
          <Badge colorPalette="teal">Available for collaboration</Badge>
          <Link href="/about" color="blue.500" fontWeight="semibold">
            View profile
          </Link>
        </HStack>
      </Stack>
    </Box>
  )
}
```

### Code example 2

*Topic: 15. V2 provider syntax, for migration comparison only*

This belongs in a Chakra UI v2 project. Do not copy it into the v3 setup from this guide.

```jsx
import { ChakraProvider, extendTheme } from "@chakra-ui/react"
import App from "./App"

const theme = extendTheme({
  colors: {
    brand: {
      500: "#6d5dfc",
    },
  },
})

export function LegacyRoot() {
  return (
    <ChakraProvider theme={theme}>
      <App />
    </ChakraProvider>
  )
}
```

### Code example 3

*Topic: 15. V3 provider syntax*

This is the matching v3 setup using the default system. If you created a custom system in the [theming lesson](03-theming.md), pass that system instead.

```jsx
import { ChakraProvider, defaultSystem } from "@chakra-ui/react"
import App from "./App"

export function Root() {
  return (
    <ChakraProvider value={defaultSystem}>
      <App />
    </ChakraProvider>
  )
}
```

## All Q&A in this chapter

### 1. Which areas should you review when migrating from Chakra UI v2 to v3?

Review provider and theme setup, changed component composition and props, and color-mode imports. Then check the official migration guide and test the interface at common breakpoints.

### 2. How do you add a responsive list of skills to the profile card?

Put skill badges in an `HStack` with `wrap="wrap"` and a gap. They stay on one line when space allows and wrap onto another line on narrower screens, as shown in Code example 1.

### 3. How do you make the profile action a real, accessible link?

Use Chakra's `Link` with an `href` and visible text such as `View profile`. The text supplies its accessible name and the `href` gives it normal link behavior.

### 4. How do you investigate missing styles from a provider or system issue?

Check that the app is wrapped once in `ChakraProvider`, that its `value` is the intended system, and that custom token names match the theme. Also check the browser console for provider or token errors.

### 5. How do you test keyboard focus on the profile card?

Use Tab and Shift+Tab to move through the link and other controls. Confirm the focused control is visibly highlighted and that the order follows the visual reading order.

---

| [← Previous: Color mode and recipes](05-color-mode-and-recipes.md) | [Next: Official references →](references.md) |
|:--|--:|
