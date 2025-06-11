---
title: Toast Notification System Documentation
author: Krish Vishwakarma
date: 2025-06-05 11:25:00 +0530
categories: [Web Dev, Tutorial]
tags: [php, UIUX]
---

# Toast Notification System Documentation

## Overview
The [`toast.php`](https://gist.github.com/ExtremeKrish/d99a0bceffd3d5c4bfb928c886c997bf) file provides a reusable toast notification system for PHP applications. It supports multiple toast types (primary, secondary, info, danger, success, warning), each with a corresponding icon and color. Include the file in your PHP project to use the `Toast` class in JavaScript for displaying notifications.

## Installation
1. Save the `toast.php` file in your project directory (e.g., `includes/toast.php`).
2. Include it in your PHP file:
   ```php
   <?php require 'includes/toast.php'; ?>
   ```
3. Ensure your PHP file outputs within an HTML structure (e.g., `<body>`).

## Usage
The `Toast` class is globally available in JavaScript after including `toast.php`. Create an instance of `Toast` and call its `show` method to display toasts.

### Methods
The `Toast` class provides one main method to display toasts:

#### `show({ message, type, duration, position })`
Displays a toast notification with a message, type-specific icon, and color.

- **Parameters**:
  - `message` (string): The message to display in the toast.
  - `type` (string, default: `'primary'`): The type of toast. Options: `'primary'`, `'secondary'`, `'info'`, `'danger'`, `'success'`, `'warning'`.
  - `duration` (number, default: `3000`): Duration in milliseconds before the toast auto-closes.
  - `position` (string, default: `'top-right'`): Position of the toast container. Options: `'top-right'`, `'top-left'`, `'bottom-right'`, `'bottom-left'`.
- **Example**:
  ```javascript
  const toast = new Toast();
  toast.show({
    message: 'Operation completed successfully!',
    type: 'success',
    duration: 4000,
    position: 'top-right'
  });
  ```

### Toast Types and Icons
Each toast type has a unique icon and colored left border:
- **Primary**: `â„¹ï¸` (Info symbol, blue border: `--color-primary`)
- **Secondary**: `âš™ï¸` (Gear symbol, gray border: `--color-secondary`)
- **Info**: `ðŸ””` (Bell symbol, teal border: `--color-info`)
- **Danger**: `âŒ` (Cross symbol, red border: `--color-danger`)
- **Success**: `âœ…` (Checkmark symbol, green border: `--color-success`)
- **Warning**: `âš ï¸` (Warning symbol, yellow border: `--color-warning`)

### Features
- **Modern UI**: Uses CSS variables (`--color-background`, `--color-foreground`, `--color-border`, and type-specific colors) for a dark, minimal theme with smooth slide-in animations.
- **Icons**: Each toast type includes a modern emoji icon for visual distinction.
- **Auto-Close**: Toasts disappear after the specified duration.
- **Manual Close**: Click the toast to close it immediately.
- **Positioning**: Supports four corner positions (`top-right`, `top-left`, `bottom-right`, `bottom-left`).
- **Stacking**: Multiple toasts stack vertically (top-down for top positions, bottom-up for bottom positions).

### Example Integration
Create a PHP file (e.g., `index.php`):
```php
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Test Toasts</title>
</head>
<body>
  <button onclick="showPrimaryToast()">Primary Toast</button>
  <button onclick="showSecondaryToast()">Secondary Toast</button>
  <button onclick="showInfoToast()">Info Toast</button>
  <button onclick="showDangerToast()">Danger Toast</button>
  <button onclick="showSuccessToast()">Success Toast</button>
  <button onclick="showWarningToast()">Warning Toast</button>

  <?php require 'includes/toast.php'; ?>

  <script>
    const toast = new Toast();

    function showPrimaryToast() {
      document.activeElement?.blur();
      toast.show({
        message: 'This is a primary toast!',
        type: 'primary',
        duration: 3000,
        position: 'top-right'
      });
    }

    function showSecondaryToast() {
      document.activeElement?.blur();
      toast.show({
        message: 'This is a secondary toast!',
        type: 'secondary',
        duration: 3000,
        position: 'top-left'
      });
    }

    function showInfoToast() {
      document.activeElement?.blur();
      toast.show({
        message: 'This is an info toast!',
        type: 'info',
        duration: 3000,
        position: 'bottom-right'
      });
    }

    function showDangerToast() {
      document.activeElement?.blur();
      toast.show({
        message: 'This is a danger toast!',
        type: 'danger',
        duration: 3000,
        position: 'bottom-left'
      });
    }

    function showSuccessToast() {
      document.activeElement?.blur();
      toast.show({
        message: 'This is a success toast!',
        type: 'success',
        duration: 3000,
        position: 'top-right'
      });
    }

    function showWarningToast() {
      document.activeElement?.blur();
      toast.show({
        message: 'This is a warning toast!',
        type: 'warning',
        duration: 3000,
        position: 'top-right'
      });
    }
  </script>
</body>
</html>
```

### Notes
- Include `toast.php` after the `<body>` tag or where the toast styles and scripts are needed.
- The toast system is self-contained and requires no external dependencies.
- Customize the CSS variables in `:root` to match your application's theme (e.g., adjust `--color-primary` for different shades).
- Toasts are not focusable by keyboard to keep them non-intrusive, but they can be closed by clicking.
- Use a single `Toast` instance for multiple toasts to maintain a single container.
