# Regular Expressions

## Regular Expressions
- Find contents of pattern: `{{'xhsgdksdhf jsjd hfsjdfh skdjfhsj fhsdkj'|t}}`
  - Regex: `\{\{'([A-Z ]+)'\|t\}\}`
- Find Arabic texts in a file:
  ```
  [^\x00-\x80]+
  ```
