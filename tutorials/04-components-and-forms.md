# Components and forms

Compose interactive v3 components and build accessible forms.

[Back to tutorial index](../README.md)

---

## 10. Compose interactive components

Many v3 components are compound components. Their parts are composed under a root component, which makes structure explicit and gives you control over the markup.

### Accordion

See [Code example 1](#code-example-1) in the code section below.

### Dialog

Use a dialog for an interruptive task that needs the user's attention. Give it a clear title, description, and actions, and ensure the close action is available.

See [Code example 2](#code-example-2) in the code section below.

Component APIs can change across major versions. When composing a component, check its current official page for required parts and props.

**Official guides:** [Component concepts](https://chakra-ui.com/docs/components/concepts/overview) · [Accordion](https://chakra-ui.com/docs/components/accordion) · [Dialog](https://chakra-ui.com/docs/components/dialog) · [Tabs](https://chakra-ui.com/docs/components/tabs) · [Menu](https://chakra-ui.com/docs/components/menu)

## 11. Build accessible forms

Use `Field` to connect labels, helper text, and validation messages to form controls. Native form elements and clear labels make forms easier to use with keyboards and assistive technology.

See [Code example 3](#code-example-3) in the code section below.

For real validation, connect the form to your chosen validation approach and show an error message that explains how to fix the problem. Do not rely on color alone to communicate error or success.

**Official guides:** [Field](https://chakra-ui.com/docs/components/field) · [Input](https://chakra-ui.com/docs/components/input) · [Checkbox](https://chakra-ui.com/docs/components/checkbox) · [Focus ring](https://chakra-ui.com/docs/styling/focus-ring) · [Skip navigation](https://chakra-ui.com/docs/components/skip-nav) · [Visually hidden content](https://chakra-ui.com/docs/components/visually-hidden)


## All code samples in this chapter

### Code example 1

*Topic: Accordion*

```jsx
import { Accordion } from "@chakra-ui/react"

export function InstallAccordion() {
  return (
    <Accordion.Root collapsible defaultValue={["installation"]}>
      <Accordion.Item value="installation">
        <Accordion.ItemTrigger>
          <span>How do I install Chakra UI?</span>
          <Accordion.ItemIndicator />
        </Accordion.ItemTrigger>
        <Accordion.ItemContent>
          <Accordion.ItemBody>
            Install @chakra-ui/react and @emotion/react, then add ChakraProvider at the app root.
          </Accordion.ItemBody>
        </Accordion.ItemContent>
      </Accordion.Item>
      <Accordion.Item value="provider">
        <Accordion.ItemTrigger>
          <span>Where does the provider go?</span>
          <Accordion.ItemIndicator />
        </Accordion.ItemTrigger>
        <Accordion.ItemContent>
          <Accordion.ItemBody>Wrap the application once near its root.</Accordion.ItemBody>
        </Accordion.ItemContent>
      </Accordion.Item>
    </Accordion.Root>
  )
}
```

### Code example 2

*Topic: Dialog*

```jsx
import { Button, Dialog, Portal } from "@chakra-ui/react"

export function ProjectDetailsDialog() {
  return (
    <Dialog.Root>
      <Dialog.Trigger asChild>
        <Button variant="outline">View details</Button>
      </Dialog.Trigger>
      <Portal>
        <Dialog.Backdrop />
        <Dialog.Positioner>
          <Dialog.Content>
            <Dialog.CloseTrigger aria-label="Close dialog" />
            <Dialog.Header>
              <Dialog.Title>Project details</Dialog.Title>
            </Dialog.Header>
            <Dialog.Body>Review the project before continuing.</Dialog.Body>
            <Dialog.Footer>
              <Dialog.CloseTrigger asChild>
                <Button>Done</Button>
              </Dialog.CloseTrigger>
            </Dialog.Footer>
          </Dialog.Content>
        </Dialog.Positioner>
      </Portal>
    </Dialog.Root>
  )
}
```

### Code example 3

*Topic: 11. Build accessible forms*

```jsx
import { useState } from "react"
import { Button, Field, Input, Stack } from "@chakra-ui/react"

function isValidEmail(value) {
  return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(value)
}

export function EmailForm() {
  const [email, setEmail] = useState("")
  const [submitted, setSubmitted] = useState(false)
  const invalid = submitted && !isValidEmail(email)

  function handleSubmit(event) {
    event.preventDefault()
    setSubmitted(true)
    if (!isValidEmail(email)) return
    window.alert(`Saved email: ${email}`)
  }

  return (
    <Stack as="form" gap="4" maxW="md" noValidate onSubmit={handleSubmit}>
      <Field.Root required invalid={invalid}>
        <Field.Label>
          Email address <Field.RequiredIndicator />
        </Field.Label>
        <Input
          type="email"
          name="email"
          autoComplete="email"
          value={email}
          onChange={(event) => setEmail(event.target.value)}
        />
        <Field.HelperText>We'll use this for account updates.</Field.HelperText>
        {invalid && <Field.ErrorText>Enter a valid email address.</Field.ErrorText>}
      </Field.Root>
      <Button type="submit" colorPalette="blue" alignSelf="start">
        Save email
      </Button>
    </Stack>
  )
}
```

The browser checks `type="email"` and `required` before submitting. The `Field` composition connects the label and helper text to the input so the control is understandable without relying on its placeholder.

## All Q&A in this chapter

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

---

| [← Previous: Theming](03-theming.md) | [Next: Color mode and recipes →](05-color-mode-and-recipes.md) |
|:--|--:|
