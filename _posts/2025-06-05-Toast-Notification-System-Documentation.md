---
title: Toast Notification System Documentation
author: Krish Vishwakarma
date: 2025-06-05 11:25:00 +0530
categories: [Web Dev, Tutorial]
tags: [php, UIUX]
---

# Dialog System Documentation

## Overview
The `dialog.php` file provides a reusable dialog system for PHP applications, including confirm, single prompt, and double prompt dialogs with a modern, minimal UI. It supports pre-filled input values with the cursor positioned at the end for editing. Include the file in your PHP project to use the `Dialog` class in JavaScript.

## Installation
1. Save the `dialog.php` file in your project directory (e.g., `includes/dialog.php`).
2. Include it in your PHP file:
   ```php
   <?php require 'includes/dialog.php'; ?>
   ```
3. Ensure your PHP file outputs within an HTML structure (e.g., `<body>`).

## Usage
The `Dialog` class is globally available in JavaScript after including `dialog.php`. Create instances of `Dialog` and call its methods to display dialogs.

### Methods
The `Dialog` class provides three methods to create different types of dialogs:

#### 1. `showConfirm({ title, message, onSubmit, onCancel, cancellable })`
Displays a confirmation dialog with a message and Confirm/Cancel buttons.

- **Parameters**:
  - `title` (string): Dialog title.
  - `message` (string): Dialog message.
  - `onSubmit` (function): Callback executed when Confirm is clicked or Enter is pressed.
  - `onCancel` (function): Callback executed when Cancel is clicked or Esc is pressed (if cancellable).
  - `cancellable` (boolean, default: `true`): If `false`, hides Cancel button and disables Esc key.
- **Example**:
  ```javascript
  const dialog = new Dialog();
  dialog.showConfirm({
    title: 'Confirm Action',
    message: 'Are you sure you want to proceed?',
    onSubmit: () => console.log('Confirmed!'),
    onCancel: () => console.log('Cancelled!'),
    cancellable: true
  });
  ```

#### 2. `showPrompt({ title, message, placeholder, value, onSubmit, onCancel, cancellable })`
Displays a dialog with a single input field, auto-focused with the cursor at the end of any pre-filled text, and Submit/Cancel buttons.

- **Parameters**:
  - `title` (string): Dialog title.
  - `message` (string): Dialog message.
  - `placeholder` (string): Placeholder text for the input field.
  - `value` (string, default: `''`): Initial value for the input field.
  - `onSubmit` (function): Callback executed with the input value when Submit is clicked or Enter is pressed.
  - `onCancel` (function): Callback executed when Cancel is clicked or Esc is pressed (if cancellable).
  - `cancellable` (boolean, default: `true`): If `false`, hides Cancel button and disables Esc key.
- **Example**:
  ```javascript
  const dialog = new Dialog();
  dialog.showPrompt({
    title: 'Edit Name',
    message: 'Please update your name:',
    placeholder: 'Your name',
    value: 'John Doe',
    onSubmit: (value) => console.log(`Updated name: ${value}`),
    onCancel: () => console.log('Prompt cancelled!'),
    cancellable: true
  });
  ```

#### 3. `showDoublePrompt({ title, message, placeholders, values, onSubmit, onCancel, cancellable })`
Displays a dialog with two input fields, auto-focusing the first input with the cursor at the end of any pre-filled text, and Submit/Cancel buttons. Pressing Enter moves focus to the next input (with cursor at end) or submits if on the last input.

- **Parameters**:
  - `title` (string): Dialog title.
  - `message` (string): Dialog message.
  - `placeholders` (array): Array of two strings for the input placeholders.
  - `values` (array, default: `['', '']`): Array of two strings for initial input values.
  - `onSubmit` (function): Callback executed with an array of input values when Submit is clicked or Enter is pressed on the last input.
  - `onCancel` (function): Callback executed when Cancel is clicked or Esc is pressed (if cancellable).
  - `cancellable` (boolean, default: `true`): If `false`, hides Cancel button and disables Esc key.
- **Example**:
  ```javascript
  const dialog = new Dialog();
  dialog.showDoublePrompt({
    title: 'Edit User Details',
    message: 'Please update your details:',
    placeholders: ['First name', 'Last name'],
    values: ['John', 'Doe'],
    onSubmit: ([first, last]) => console.log(`Updated details: ${first} ${last}`),
    onCancel: () => alert('Double prompt cancelled!'),
    cancellable: true
  });
  ```

### Features
- **Pre-filled Inputs**: Inputs can be pre-filled with initial values, and the cursor is positioned at the end for editing.
- **Auto-Focus**: Inputs (for prompt dialogs) or the Confirm button (for confirm dialogs) are focused on open.
- **Cursor Positioning**: The cursor is placed at the end of pre-filled text in input fields.
- **Enter Key**: Submits the dialog or moves to the next input (in double prompt dialogs), positioning the cursor at the end of pre-filled text.
- **Esc Key**: Closes the dialog if `cancellable` is `true`.
- **Focus Trap**: Tab and Shift+Tab navigation stays within the dialog.
- **Modern UI**: Uses CSS variables (`--color-background`, `--color-foreground`, `--color-border`) for a dark, minimal theme with smooth animations.
- **Event Isolation**: Prevents key events from affecting elements outside the dialog.

### Example Integration
Create a PHP file (e.g., `index.php`):
```php
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Test Dialogs</title>
</head>
<body>
  <button onclick="showConfirmDialog()">Show Confirm Dialog</button>
  <button onclick="showPromptDialog()">Show Prompt Dialog</button>
  <button onclick="showDoublePromptDialog()">Show Double Prompt Dialog</button>

  <?php require 'includes/dialog.php'; ?>

  <script>
    function showConfirmDialog() {
      document.activeElement?.blur();
      const dialog = new Dialog();
      dialog.showConfirm({
        title: 'Confirm Action',
        message: 'Are you sure you want to proceed?',
        onSubmit: () => alert('Confirmed!'),
        onCancel: () => alert('Cancelled!'),
        cancellable: true
      });
    }

    function showPromptDialog() {
      document.activeElement?.blur();
      const dialog = new Dialog();
      dialog.showPrompt({
        title: 'Edit Name',
        message: 'Please update your name:',
        placeholder: 'Your name',
        value: 'John Doe',
        onSubmit: (value) => alert(`Updated name: ${value}`),
        onCancel: () => alert('Prompt cancelled!'),
        cancellable: true
      });
    }

    function showDoublePromptDialog() {
      document.activeElement?.blur();
      const dialog = new Dialog();
      dialog.showDoublePrompt({
        title: 'Edit User Details',
        message: 'Please update your details:',
        placeholders: ['First name', 'Last name'],
        values: ['John', 'Doe'],
        onSubmit: ([first, last]) => alert(`Updated details: ${first} ${last}`),
        onCancel: () => alert('Double prompt cancelled!'),
        cancellable: true
      });
    }
  </script>
</body>
</html>
```

### Notes
- Include `dialog.php` after the `<body>` tag or where the dialog styles and scripts are needed.
- The dialog system is self-contained and requires no external dependencies.
- Customize the CSS variables in `:root` to match your application's theme.
- The focus retry mechanism ensures reliable focus on inputs or buttons, with the cursor positioned at the end of pre-filled text.
- Ensure pre-filled values are strings to avoid input field issues.
