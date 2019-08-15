## 7bit_ascii

Checks that your code contains only characters from the 7bit ASCII set. 

Disabled in clean variant since new systems have unicode support.

## avoid_use

Checks for usage of certain statements.

Currently supported:

- define (clean abap rule - no macros)
- endselect
- execSQL 
- kernel call
- communication
- statics (probably a clean abap rule)

`TODO this is easy to extend, check for other statements which could be added`

## breakpoint

- checks for `BREAK` and `BREAK-POINT` statements.

Should be part of clean variant, although this check could easily be merged with `avoid_use`

## check_variables

`TODO no idea what this does`

## class_attribute_names

Enables you to enforce a pattern, such as a prefix, for static and instance class member names.
Clean ABAP suggests that you eliminate prefixes.

`TODO check if globals are sometimes recommended`
`TODO check if negative lookbehinds are supported by the regex so common prefixes can be disallowed`

## cloud_types

Checks for object types incompatible with cloud abap.

```ts
if (reg.getConfig().getVersion() !== Version.Cloud
        || obj instanceof Objects.Class
        || obj instanceof Objects.Interface
        || obj instanceof Objects.MessageClass
        || obj instanceof Objects.Package
        || obj instanceof Objects.Table
        || obj instanceof Objects.TableType
        || obj instanceof Objects.DataDefinition
        || obj instanceof Objects.DataControl
        || obj instanceof Objects.LockObject
        || obj instanceof Objects.Transformation
        || obj instanceof Objects.FunctionGroup
        || obj instanceof Objects.DataElement
        || obj instanceof Objects.Domain) {
return [];

```

```TODO make cloud ABAP variant as well```


## colon_missing_space

Checks for a missing space after a colon in chained statements.

Example:

```abap
" incorrect
WRITE:`abc`.

"correct
WRITE: `abc`.
```

This is correct indentation and is part of the clean variant.

## commented_code

Checks for commented out code. You should not generally leave commented out code so it is good that you are warned about it. This rule is part of the clean variant.

## constructor_visibility_public

Enabled in clean variant
`TODO link to clean abap section on this`

## contains_tab

Checks for tabs in your code. Enable it yourself if you want to enforce usage of spaces.

## definitions_top

Enforces that data and field-symbol definitions are on top of the method. While sometimes good for readability, it is an antipattern as variables should be declared inline or close to their first declaration. Disabled by default.

## description_empty

Checks for empty descriptions in the abapgit xml metadata. While not part of abap, this helps ensure the consistency of your serialized files. Enabled by default.

## double_space

I think this ensures that there is a `single` space after certain keywords and parentheses. Good indentation practice, enabled.

List of keywords can be extended, see
https://github.com/abaplint/abaplint//blob/ba4c6f8d03eb8d1a31c277d06c9d9cb9e7ad86b8/src/rules/whitespace/double_space.ts#L42


## empty_line_in_statement

`TODO try this out`

## empty_statement

Sounds very much like empty_line_in_statement

`TODO try this out`


## empty_structure

Checks for certain empty code blocks. All enabled by default.

Can be extended:
https://github.com/abaplint/abaplint//blob/8d29328ecc5e9c6df44b681504e6dd899abffc84/src/rules/empty_structure.ts#L16

## exit_or_check

Checks for `EXIT` and `CHECK` statements outside of loops.

`TODO I think clean abap allows check at the beginning. Disabled for now`

## exporting

Checks for EXPORTING statements which can be omitted from method calls. This is a good practice, enabled by default.

## functional_writing

Checks that method calls use the functional `method()` style instead of `CALL METHOD method` if possible. Enabled by default.

## global_class

Mostly checks abapgit metadata for class names. The situations checked for are caused by code which can't be activated, but the rule is enabled for some extra validation.