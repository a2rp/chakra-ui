[Back to tutorial index](../README.md)

# All Questions and Answers

A complete collection of questions and answers from every Chakra UI tutorial chapter.

## Getting started

### 1. What does ChakraProvider make available, and where does it go?

It makes Chakra's system, theme values, and styling context available to descendant components. Wrap the app once near its root so every page can use the same configuration.

### 2. Which packages are needed for a basic setup?

Install `@chakra-ui/react` and `@emotion/react`. Add other packages such as `next-themes` when you set up color mode.

### 3. How do you build a welcome panel?

Compose `Heading`, `Text`, and `Button` inside a `Stack`, as shown in Code example 4. Use a semantic token such as `fg.muted` for supporting text.

### 4. How do you add Chakra UI when the app already has a root provider?

Install the packages and nest ChakraProvider inside the existing app provider. Keep the existing React root and avoid wrapping the application in a second `createRoot`.

### 5. Why check the Chakra UI major version before copying a tutorial?

Major versions can change provider props, component composition, and color-mode APIs. A v2 snippet may fail or behave differently in a v3 project.

## Styling and layout

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

## Theming

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

## Components and forms

### 1. What makes a component compound, and what does its Root part coordinate?

A compound component is built from related parts, such as `Accordion.Root`, `Accordion.Item`, and `Accordion.ItemTrigger`. The Root coordinates shared state and behavior for those parts.

### 2. How do you add a second accordion item?

Add another `Accordion.Item` with a distinct `value`, then give it its own trigger and content. Code example 1 includes both `installation` and `provider` items.

### 3. What should an accessible dialog provide, and how can it close?

Give it a clear title, useful description, and named actions. The example includes a labeled close control; Chakra also closes the dialog with Escape by default.

### 4. How do you build a required email field with helper and error text?

Use `Field.Root required`, a `Field.Label`, and an `Input` with `type="email"`. Set the field's `invalid` prop after validation and render `Field.ErrorText`, as shown in Code example 3.

### 5. Why should errors not be communicated by color alone?

Some users cannot distinguish the colors, and color may not be exposed to assistive technology. Pair color with a clear message and an accessible invalid state.

## Color mode and recipes

### 1. What role does `next-themes` play in Chakra UI v3 color mode?

It manages the active light or dark theme and exposes it to the app. Chakra's generated provider connects it to Chakra's styling system, while semantic tokens resolve to the appropriate colors.

### 2. Why can a v2 `useColorMode` example fail in a v3 project?

The v3 hook is supplied by the generated color-mode snippet, not imported from `@chakra-ui/react` as in older examples. Add the snippet and import the helper from its generated file.

### 3. When is a component recipe useful?

Use a recipe when a component needs shared base styles and repeatable variants or sizes. It keeps the visual rules in one place instead of duplicating them at each use.

### 4. What do the Chakra CLI snippet and typegen commands do?

The snippet command adds reusable component or provider code. `typegen` generates TypeScript typings for custom tokens and recipes, enabling safer autocomplete; it is optional for JavaScript-only projects.

### 5. What should you keep from a generated provider snippet?

Keep the Chakra provider, the color-mode provider if the app needs theme switching, and any color-mode controls or helpers you use. Remove unused generated UI pieces and keep only one root provider.

## Migration and practice

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

| [← Previous: Migration and practice](06-migration-and-practice.md) | [Next: Official references →](references.md) |
|:--|--:|
