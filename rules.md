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

https://github.com/SAP/styleguides/blob/master/clean-abap/CleanABAP.md#if-your-global-class-is-create-private-leave-the-constructor-public

Enabled.

## contains_tab

Checks for tabs in your code. Enable it yourself if you want to enforce usage of spaces.

## definitions_top

Enforces that data and field-symbol definitions are on top of the method. While sometimes good for readability, it is an antipattern as variables should be declared inline or close to their first declaration. 

Disabled.

## description_empty

Checks for empty descriptions in the abapgit xml metadata. While not part of abap, this helps ensure the consistency of your serialized files. 

Enabled.

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

## identical_form_names

Checks for identically named forms. Form usage is discouraged in general. Enabled by default.

## if_in_if

https://github.com/SAP/styleguides/blob/master/clean-abap/CleanABAP.md#keep-the-nesting-depth-low

## in_statement_indentation

Another check for redundant spacing. Enabled by default.

## indentation

`todo try out`

## inline_data_old_versions

Checks for inline data declarations in releases which are unavailable.

`possibly this is redundant, as you can specify the language version`

## keywords_upper

Checks that keywords are in uppercase. Parameters allow to skip certain parts of code such as class definitions, which can be reformatted by SE80. 

Enable it yourself if this is your preferred convention.

## line_length

Enabled by default. 120 is the perscribed preferable length:

https://github.com/SAP/styleguides/blob/master/clean-abap/CleanABAP.md#stick-to-a-reasonable-line-length

## line_only_punc

Checks for lines containing only . or ).
Enable it yourself if this is your preferred convention.

## local_class_naming

Enables you to enforce a pattern, such as a prefix, for local as well as test classes.
Clean ABAP suggests that you eliminate prefixes, but for local classes it is very common. For now not included.

This example has prefixes:
https://github.com/SAP/styleguides/blob/master/clean-abap/CleanABAP.md#call-local-test-classes-by-their-purpose

`TODO check if negative lookbehinds are supported by the regex so common prefixes can be disallowed`

## local_variable_names

Enables you to enforce a pattern, such as a prefix, for local variables, constants and field symbols.
Clean ABAP suggests that you eliminate prefixes.

`TODO check if negative lookbehinds are supported by the regex so common prefixes can be disallowed`

## max_one_statement

Checks that code only contains one statement per line. Enabled by default.

## message_exists

Checks that a message class and id exists. Enabled by default.

## method_length

https://github.com/SAP/styleguides/blob/master/clean-abap/CleanABAP.md#keep-methods-small says 3-5 statements, which would raise a lot of violations. The number 25 is also used often (fits within one screen), for now I am using it a a sane max limit.

## method_parameter_names

Enables you to enforce a pattern, such as a prefix, for method parameter names.
Clean ABAP suggests that you eliminate prefixes. For now not enabled.

`TODO check if negative lookbehinds are supported by the regex so common prefixes can be disallowed`

## mix_returning

Checks that only one returning/exporting/changing parameter is present per method in total.

https://github.com/SAP/styleguides/blob/master/clean-abap/CleanABAP.md#use-either-returning-or-exporting-or-changing-but-not-a-combination

Enabled.

## msag_consistency

Checks serialized message classes.

- id is 3 digit
- text exists

Enabled.

## nesting

Checks for code exceeding a maximum nesting depth.

An exact maximum is not defined in clean abap, but I believe 5 is used in ATC. Note that in most cases you shouldn't go above 2.

https://github.com/SAP/styleguides/blob/master/clean-abap/CleanABAP.md#keep-the-nesting-depth-low

Enabled.

## obsolete_statement

I think it is the same thing as avoid_use. Includes `refresh`, `compute`, `add`, `subtract`, `multiply`, `move`, `divide`, `requested`.

Enabled

## parser_error

Report abaplint failures. You should log these as issues on https://github.com/abaplint/abaplint/issues so that they can be fixed.

Enabled

## preferred_compare_operators

Checks for usage of the operators listed in `badOperators`.

Enabled for comparison operators.


## remove_descriptions

`TODO Not sure of the purpose for this.`

Disabled.

## sequential_blank

Checks for redundant spaces.

`TODO might be duplicate with some other punctuation checks.`

Enabled.

## short_case

Checks for `case` statements which have fewer than `length` branches. At the very least, you shouldn't have one.

`todo not sure what allow here does`

Enabled, default 2.

## space_before_colon

`TODO There's also colon_missing_space. Duplicate?`

Disabled.

## space_before_dot

`TODO Seems like many whitespace checks are for similar things.`

Disabeld.

## start_at_tab

Ensures code starts at tabstop positions.

Disabled. Enable if you want to enforce tabs.

## superclass_final

Checks for final classes which are inherited from. This does not pass syntax checks, but possibly makes sense to check in serialized code.

Enabled.

## tabl_enhancement_category

`todo read up on this`

## unreachable code

Checks for unreachable code - lines after a `RETURN`, `EXIT` or `RAISE`. Raising exceptions might have a few false positives.

Enabled, please report false positives.

## use_new

Checks for `CREATE OBJECT` statements. You should replace these with `NEW`.

Enabled.

## when_others_last

Checks that `WHEN OTHERS` is the last case of a switch statement.

Enabled.

## whitespace_end

Checks for whitespace at the end of a line.

Enabled.