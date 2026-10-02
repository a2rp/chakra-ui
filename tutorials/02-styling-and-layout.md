# Styling and layout

Learn style props, layout primitives, and mobile-first responsive design.

[Back to tutorial index](../README.md)

---

## 5. Style with props

Style props map common CSS properties to concise component props. They accept the design-system values configured by your theme.

See [Code example 1](#code-example-1) in the code section below.

Common props include:

| Goal | Common props |
| --- | --- |
| Spacing | `p`, `px`, `py`, `pt`, `m`, `mx`, `gap` |
| Size | `w`, `h`, `minW`, `maxW`, `minH`, `maxH` |
| Layout | `display`, `position`, `alignItems`, `justifyContent`, `flex`, `gridTemplateColumns` |
| Type | `fontSize`, `fontWeight`, `lineHeight`, `letterSpacing`, `textAlign` |
| Surface | `bg`, `color`, `borderWidth`, `borderColor`, `borderRadius`, `boxShadow` |

Use the [styling overview](https://chakra-ui.com/docs/styling/overview) as a reference when you need the exact property name or supported values.

## 6. Create layouts

Chakra provides layout primitives that make common flex and grid patterns easier to compose.

### Stack

Use `Stack` for one-dimensional layouts with consistent spacing.

See [Code example 2](#code-example-2) in the code section below.

### Flex

Use `Flex` when you need direct control of alignment and distribution.

See [Code example 3](#code-example-3) in the code section below.

### Grid

Use `Grid` or `SimpleGrid` for two-dimensional layouts.

See [Code example 4](#code-example-4) in the code section below.

**Official guides:** [Box](https://chakra-ui.com/docs/components/box) · [Flex](https://chakra-ui.com/docs/components/flex) · [Grid](https://chakra-ui.com/docs/components/grid) · [Stack](https://chakra-ui.com/docs/components/stack) · [Container](https://chakra-ui.com/docs/components/container)

## 7. Make layouts responsive

Chakra's responsive styles are mobile-first. A value under `base` applies by default, then a larger breakpoint can override it.

See [Code example 5](#code-example-5) in the code section below.

Default breakpoints are `base`, `sm`, `md`, `lg`, `xl`, and `2xl`. Breakpoint values can be used with style props, visibility props, and layout props. Start with the narrow-screen layout, then add overrides where the content needs them.

**Official guide:** [Responsive design](https://chakra-ui.com/docs/styling/responsive-design)


## All code samples in this chapter

### Code example 1

*Topic: 5. Style with props*

```jsx
import { Box, Text } from "@chakra-ui/react"

export function Notice() {
  return (
    <Box
      bg="blue.subtle"
      borderWidth="1px"
      borderColor="blue.muted"
      borderRadius="xl"
      p="5"
      maxW="md"
    >
      <Text fontWeight="semibold">Deployment complete</Text>
      <Text color="fg.muted" mt="1">
        Your latest changes are now available.
      </Text>
    </Box>
  )
}
```

### Code example 2

*Topic: Stack*

```jsx
import { Button, Stack } from "@chakra-ui/react"

export function StackActions() {
  return (
    <Stack direction="row" gap="3" wrap="wrap">
      <Button variant="outline">Cancel</Button>
      <Button colorPalette="blue">Continue</Button>
    </Stack>
  )
}
```

### Code example 3

*Topic: Flex*

```jsx
import { Box, Flex } from "@chakra-ui/react"

export function ProjectSummary() {
  return (
    <Flex align="center" justify="space-between" gap="4">
      <Box>Project details</Box>
      <Box color="fg.muted">Updated today</Box>
    </Flex>
  )
}
```

### Code example 4

*Topic: Grid*

```jsx
import { Box, SimpleGrid, Text } from "@chakra-ui/react"

export function ProjectGrid() {
  return (
    <SimpleGrid columns={{ base: 1, md: 2, xl: 3 }} gap="5">
      {["Notes app", "Portfolio", "Task tracker"].map((name) => (
        <Box key={name} borderWidth="1px" borderRadius="lg" p="5">
          <Text fontWeight="semibold">{name}</Text>
          <Text color="fg.muted" mt="2">A small project card.</Text>
        </Box>
      ))}
    </SimpleGrid>
  )
}
```

### Code example 5

*Topic: 7. Make layouts responsive*

```jsx
import { Box, Heading, SimpleGrid, Text } from "@chakra-ui/react"

export function ResponsiveProjects() {
  const projects = ["Notes app", "Portfolio", "Task tracker"]

  return (
    <Box px={{ base: "4", md: "8" }} py={{ base: "6", lg: "12" }}>
      <Heading fontSize={{ base: "2xl", md: "4xl" }}>Projects</Heading>
      <Text mt="2" maxW="2xl" color="fg.muted">
        A collection of recent work.
      </Text>
      <SimpleGrid columns={{ base: 1, sm: 2, lg: 3 }} gap={{ base: "4", lg: "6" }} mt="8">
        {projects.map((project) => (
          <Box key={project} borderWidth="1px" borderRadius="lg" p="5">
            <Heading size="md">{project}</Heading>
            <Text mt="2" color="fg.muted">Built with React and Chakra UI.</Text>
          </Box>
        ))}
      </SimpleGrid>
    </Box>
  )
}
```

## All Q&A in this chapter

### 1. What is a Chakra style prop? Give three examples.

A style prop applies a CSS style through a Chakra component prop. For example, `p` sets padding, `bg` sets the background color, and `fontSize` sets the text size.

### 2. When do you choose Stack, Flex, or Grid?

Use `Stack` for items arranged in one direction with a consistent gap, `Flex` for direct control over alignment and distribution, and `Grid` for rows and columns.

### 3. How do you make a responsive card grid?

Set `columns={{ base: 1, md: 2, lg: 3 }}` on `SimpleGrid`. The layout uses one column by default, two from the `md` breakpoint, and three from `lg`.

### 4. Why use design tokens instead of repeating arbitrary values?

Tokens keep spacing and colors consistent across the app. Changing a shared token later updates every component that uses it.

### 5. What should you check at the base, md, and lg breakpoints?

Check that content fits without horizontal scrolling, text remains readable, controls have enough room, and the number of columns suits the available width. Adjust padding, type size, or columns when the layout feels cramped.

---

| [← Previous: Getting started](01-getting-started.md) | [Next: Theming →](03-theming.md) |
|:--|--:|
