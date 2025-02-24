# JSON Schema / tsoa keyword annotations

Under the hood, OpenAPI heavily relies on JSON Schema Draft 00 for all the data model specifications.
JSON Schema Draft 00 defines data types that are not implemented in TypeScript.
A great example are integers.
If we want to communicate that a number must be an integer,
tsoa will specify this in the OAS and validate incoming requests against that.

::: warning
As always, _\$ref_ restrictions apply
:::

In general, the JSDoc notation is very similar each time:

```
@<keyword> <argument>* <rejectionMessage>?
```

Examples:

```typescript {3,4,8,12}
interface CustomerDto {
    /**
     * @isInt we would kindly ask you to provide a number here
     * @minimum 18 minimum age is 18
     */
    age: number;
    /**
     * @minItems 1 at least 1 category is required
     */
    tags: string[];
    /**
     * @pattern ^(.+)@(.+)$ please provide correct email
     */
    email: string;
}
```

::: tip
For parameters, use the `@<keyword> <paramName> <argument>* <rejectionMessage>?` syntax in your JSDoc (similar to [descriptions](#parameter-descriptions) or [examples](#parameter-examples))
:::

## List of supported keywords (with arguments)

[Click here for the list of keywords supported by OpenAPI 3](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.3.md#properties)

### Generic

- `@default`
- `@format`

::: danger
Formats will generally not be validated, except for `format: date(time)`, which will automatically be generated for TS type `Date`.
:::

### Date

- `@isDateTime <errMsg>` for setting custom error messages
- `@isDate <errMsg>` for setting custom error messages
- `@minDate <errMsg>`
- `@maxDate <errMsg>`

### Numeric

- `@isInt <errMsg>` **tsoa special** since TS does not know integer as a type
- `@isFloat <errMsg>` **tsoa special** since TS does not know integer as a type
- `@isLong <errMsg>`
- `@isDouble <errMsg>`
- `@minimum <number> <errMsg>`
- `@maximum <number> <errMsg>`

### String

- `@isString <errMsg>` for setting custom error messages
- `@minLength <number> <errMsg>`
- `@maxLength <number> <errMsg>`
- `@pattern <regex> <errMsg>`

### Array

- `isArray <errMsg>` for setting custom error messages
- `minItems <number> <errMsg>`
- `maxItems <number> <errMsg>`
- `uniqueItems <errMsg>`

### Boolean

- `isBool <errMsg>` for setting custom error messages
