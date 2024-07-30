# Common Language Style Guide

## Capitalization

The following terms describe different forms of capitalization

- StudlyCase
- camelCase
- UPPER_CASE
- snake_case
- kebab-case

If an identifier contains more than one word, do not use underscores ( _ ) or hyphens ( - ), except when the identifier is using UPPER_CASE or snake_case.

| Identifier          | Casing     |
|---------------------|------------|
| Class               | StudlyCase |
| Interface           | StudlyCase |
| Enum Type           | StudlyCase |
| Enum Value          | StudlyCase |
| Constants           | UPPER_CASE |
| Properties          | camelCase  |
| Method Parameters   | camelCase  |
| Methods Names       | camelCase  |
| Function Name       | snake_case |
| Function Parameters | camelCase  |


## Variable Naming

Variables should always be named descriptively and concisely. Single character variables should never be used unless otherwise specified in a language
specific style guide.

#### Bad Variable Naming

```php
foreach ($items as $i) {
    //do things in the iteration
}
```

#### Good Variable Naming

```php
foreach ($items as $item) {
    //do things in the iteration
}
```

## Other Scenarios

If you encounter a scenario not covered here, please refer to the language-specific style guide. Please open a PR detailing your proposed solution if
the scenario is still not covered.
