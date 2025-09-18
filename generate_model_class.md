### General-Purpose Prompt for Creating DTOs and Models

You can copy and paste this entire template and simply replace the parts in `[brackets]` with your specific feature details.

-----

  * `[feature_name]` becomes `product`.
  * `[FeatureName]` becomes `Product`.
    
**ROLE:** You are an expert Flutter/Dart developer specializing in clean architecture and data modeling.

**TASK:** Your goal is to create two separate Dart files: one for Data Transfer Objects (DTOs) and one for the corresponding Domain Models, based on the JSON data structure I provide.

**INSTRUCTIONS & CONVENTIONS:**

1.  **File Generation:**

      * Create a DTO file named `[feature_name]_dto.dart`.
      * Create a Model file named `[feature_name]_model.dart`.

2.  **Naming Conventions:**

      * The main class name should be `[FeatureName]DTO` and `[FeatureName]Model`.
      * For any nested JSON objects, create corresponding child classes. The naming must follow the pattern `[FeatureName][ChildObjectName]DTO` and `[FeatureName][ChildObjectName]Model`.

3.  **DTO File (`[feature_name]_dto.dart`):**

      * This file must contain all DTO classes related to the feature.
      * Each DTO class must include a `factory YourDTO.fromJson(Map<String, dynamic> json)` constructor.
      * Properties in the DTO should match the JSON keys (use `@JsonKey` for `snake_case` if needed, though direct mapping is fine).
      * Make properties nullable if they can be `null` in the JSON response.
      * Each DTO class must include a `toDomain()` method that converts the DTO instance into its corresponding Model instance.
      * Handle data type conversions within the `fromJson` and `toDomain` methods (e.g., converting date strings to `DateTime`, integers to `bool`).

4.  **Model File (`[feature_name]_model.dart`):**

      * This file must contain all Model classes related to the feature.
      * Models should represent the clean data structure for use within the app.
      * Use app-friendly data types (e.g., `DateTime`, `bool`, `enum`).
      * Models should **NOT** contain `fromJson` or `toDomain` methods.

5.  **JSON Parsing Context:**

      * Ignore any standard API response wrappers in the JSON (like `status`, `message`, `data`, `error`).
      * Focus only on the structure of the objects **inside** the `data` array or field.

-----

**INPUT JSON FOR `[FeatureName]`:**

```json
[Paste your JSON structure here]
```

-----

### **Example Usage:**

Let's say you have a new feature called **Product**.

**1. Fill in the `[brackets]`:**

  * `[feature_name]` becomes `product`.
  * `[FeatureName]` becomes `Product`.

**2. Paste your JSON:**

**INPUT JSON FOR `Product`:**

```json
{
  "id": 101,
  "product_name": "Wireless Mouse",
  "price": 29.99,
  "in_stock": 1,
  "details": {
    "brand": "TechCorp",
    "color": "Black"
  }
}
```

By providing this filled-in prompt, the AI would generate:

1.  `product_dto.dart`: Containing `ProductDTO` and `ProductDetailsDTO`, each with `fromJson` and `toDomain` methods.
2.  `product_model.dart`: Containing `ProductModel` and `ProductDetailsModel` with clean data types (`bool` for `inStock`, etc.).
