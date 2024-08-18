
# Android Compose Keyboard Visibility

[![](https://jitpack.io/v/sitharaj88/android-compose-keyboard-visibility.svg)](https://jitpack.io/#sitharaj88/android-compose-keyboard-visibility)

This library provides a Jetpack Compose-based solution to detect the visibility of the on-screen keyboard in Android applications.

## Features
- Detect when the keyboard is visible or hidden.
- Simple API for integration with Compose UIs.
- Handles IME actions such as "Done" to hide the keyboard.

## Installation

To use this library in your project, add the following to your `build.gradle.kts`:

### Step 1: Add JitPack to your repositories

```kotlin
repositories {
    maven { url = uri("https://jitpack.io") }
}
```

### Step 2: Add the dependency

```kotlin
dependencies {
    implementation("com.github.sitharaj88:android-compose-keyboard-visibility:1.0.0")
}
```

## Usage

Here’s a simple example of how to use the `rememberKeyboardVisibility` function:

```kotlin
import androidx.compose.foundation.layout.*
import androidx.compose.foundation.text.BasicTextField
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Modifier
import androidx.compose.ui.text.input.TextFieldValue
import androidx.compose.ui.unit.dp

@Composable
fun KeyboardVisibilityDemo() {
    val isKeyboardVisible by rememberKeyboardVisibility()
    var text by remember { mutableStateOf(TextFieldValue("")) }

    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(16.dp)
    ) {
        BasicTextField(
            value = text,
            onValueChange = { text = it },
            modifier = Modifier.fillMaxWidth(),
            keyboardOptions = KeyboardOptions.Default.copy(
                imeAction = ImeAction.Done
            ),
            keyboardActions = KeyboardActions(
                onDone = {
                    keyboardController?.hide() // Hide the keyboard when "Done" is pressed
                }
            )
        )

        Spacer(modifier = Modifier.height(16.dp))

        Text(
            text = if (isKeyboardVisible) "Keyboard is visible" else "Keyboard is hidden",
            style = MaterialTheme.typography.body1
        )
    }
}
```

## License

This library is licensed under the Apache License 2.0. See the [LICENSE](LICENSE) file for details.

## Author

Developed and maintained by **Sitharaj Seenivasan**.
