# Code Commenting Guide & Snippets

A practical guide for writing clean, maintainable, and professional comments in Dart.

## Quick Reference / TL;DR

**Documentation (`///`): For public APIs (classes, methods).**

```dart
/// A brief, single-sentence summary of what this does.
///
/// A more detailed paragraph explaining the purpose, usage, and any
/// important side effects or exceptions.
```

**Large Section Header (`//`): To organize large files.**

```dart
// ===========================================================================
// SECTION TITLE
// ===========================================================================
```

**Simple Section Header (`//`): To group related code blocks.**

```dart
// --- Group Title ---
```

**Explanatory Comment (`//`): Explains *WHY*, not *what*.**

```dart
// Using algorithm X because it handles edge cases A and B efficiently.
```

**Task Comment (`//`): For actionable items.**

```dart
// TODO: Refactor this to use the new UserService.
// FIXME: This logic fails when the input is negative.
```

**Warning Comment (`//`): For critical information.**

```dart
// IMPORTANT: This method has side effects and should not be called in a loop.
```

-----

## The Philosophy

The golden rule is: **Comments should explain *why* the code exists, not *what* it does.** Well-written code should be self-explanatory about *what* it's doing. The comments fill in the blanks about business logic, trade-offs, and purpose.

-----

## Comment Types in Detail

### 1\. Documentation Comments (`///`)

Used for any public-facing class, method, or property. Dart's `dartdoc` tool uses these to generate project documentation, and your IDE uses them for tooltips.

  * Start with a single-sentence summary.
  * Follow with a more detailed paragraph if necessary.
  * Use markdown for formatting (e.g., `[ClassName]` to create links).
  * For functions, describe what it does, its parameters (`@param`), and what it returns (`@returns`).

**Example:**

```dart
/// Fetches and manages user data for the application.
///
/// This service provides methods to get user profiles, update user settings,
/// and handle user authentication states. It acts as an abstraction layer
/// over the remote data source.
class UserService {
  /// Retrieves a user profile by their unique ID.
  ///
  /// Throws a `UserNotFoundException` if no user exists with the given [userId].
  Future<User> fetchUserById(String userId) {
    // ... implementation
  }
}
```

### 2\. Sectioning & Header Comments (`//`)

These organize code into logical, scannable sections, acting like signposts to help developers navigate large files quickly.

#### A. Large Section Headers

Multi-line comment blocks that separate major sections within a class (e.g., state, lifecycle methods, UI actions). They create a strong visual separation, making the code's architecture obvious.

  * Use a consistent, highly visible format.
  * Keep the title concise and in all caps.
  * Best used in files over \~100 lines long.

**Example:**

```dart
class UserSettingsViewModel extends ViewModel {
  // ===========================================================================
  // OBSERVABLE STATE
  // ===========================================================================
  final isLoading = ValueNotifier<bool>(true);
  final username = ValueNotifier<String>('');

  // ===========================================================================
  // LIFECYCLE METHODS
  // ===========================================================================
  @override
  void init() {
    super.init();
    loadInitialSettings();
  }
}
```

#### B. Simple Sectioning Comments

A simple one-line comment for smaller groupings. It's less visually heavy but still provides clear context.

**Example:**

```dart
class ServiceLocator {
  void setup() {
    // --- Core ---
    registerSingleton<ApiClient>(ApiClient());

    // --- Repositories ---
    registerLazySingleton<UserRepository>(/* ... */);

    // --- ViewModels ---
    registerFactory<ProfileViewModel>(/* ... */);
  }
}
```

### 3\. Explanatory Comments (`//`)

Inline comments that clarify specific lines or blocks of code.

#### A. The "Why" Comment

Explains complex algorithms, business rules, or non-obvious workarounds.

  * **Bad (Explains the *what*):**
    ```dart
    // Increment the counter
    i++;
    ```
  * **Good (Explains the *why*):**
    ```dart
    // Invalidate the session token here because the security policy
    // requires a fresh token after a password change.
    invalidateSessionToken(user.id);
    ```

#### B. The "Decision" Comment

Explains why a particular approach was taken over an alternative, providing context on technical trade-offs.

**Example:**

```dart
// Using a standard `Map` here instead of a custom class for performance.
// The lookup speed is critical, and a Map is highly optimized for this.
final userPermissions = {'admin': true, 'editor': false};
```

### 4\. Warning & Task Comments (`//`)

These draw special attention to critical information or pending work.

#### A. Admonition / Warning Comments (`// IMPORTANT:`, `// NOTE:`)

Warn other developers about critical side effects, non-obvious requirements, or potential pitfalls.

**Example:**

```dart
// IMPORTANT: Do not await this function. It's designed to run in the
// background, and awaiting it will block the UI thread.
unawaited(sendAnalyticsEvents());
```

#### B. Task Comments (`// TODO:`, `// FIXME:`)

Conventional markers often highlighted by IDEs, making them easy to find and track.

  * **`// TODO:`** Marks planned features or incomplete implementations.
      * **Example:** `// TODO: Implement pagination when the API supports it.`
  * **`// FIXME:`** Marks known bugs or code that needs correction.
      * **Example:** `// FIXME: This calculation is off by 1 in leap years.`

### Style & Formatting

#### The Vertical Line (Code Ruler)

The vertical line in your editor is a **style guide ruler** (often at 80 or 100 characters). It encourages writing code and comments that are readable without horizontal scrolling.

  * **Don't do this:**
    ```dart
    // This is a very long comment that goes on and on and forces the developer to scroll horizontally to read the entire thing, which is bad for readability and code reviews.
    ```
  * **Do this (Wrap your comments):**
    ```dart
    // This is a long comment that has been properly wrapped to respect
    // the line length guide, making it much easier to read.
    ```

#### Core Principles

  * **Be Professional:** Write clear, grammatically correct comments.
  * **Maintain Your Comments:** An incorrect, outdated comment is worse than no comment. If you change the code, update the comment.
  * **Don't Comment Bad Code, Rewrite It:** If code is so complex it needs a multi-paragraph essay to explain, the priority should be to refactor the code itself to be simpler.
