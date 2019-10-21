# Rule descriptions
- [Rule descriptions](#rule-descriptions)
  - [Code structure](#code-structure)
    - [nesting](#nesting)
    - [definitions_top](#definitions_top)
    - [no_public_attributes](#no_public_attributes)
    - [unreachable code](#unreachable-code)
    - [when_others_last](#when_others_last)
    - [exit_or_check](#exit_or_check)
    - [constructor_visibility_public](#constructor_visibility_public)
    - [short_case](#short_case)
    - [max_one_statement](#max_one_statement)
    - [method_length](#method_length)
    - [if_in_if](#if_in_if)
    - [line_length](#line_length)
  - [Documentation](#documentation)
    - [abapdoc](#abapdoc)
  - [Syntax/object usage](#syntaxobject-usage)
    - [obsolete_statement](#obsolete_statement)
    - [functional_writing](#functional_writing)
    - [avoid_use](#avoid_use)
    - [breakpoint](#breakpoint)
    - [use_new](#use_new)
    - [preferred_compare_operators](#preferred_compare_operators)
    - [mix_returning](#mix_returning)
    - [superclass_final](#superclass_final)
    - [cloud_types](#cloud_types)
    - [allowed_object_types](#allowed_object_types)
    - [inline_data_old_versions](#inline_data_old_versions)
    - [form_tables_obsolete](#form_tables_obsolete)
    - [type_form_parameters](#type_form_parameters)
  - [Redundant code](#redundant-code)
    - [commented_code](#commented_code)
    - [empty_structure](#empty_structure)
    - [exporting](#exporting)
  - [Naming conventions](#naming-conventions)
    - [class_attribute_names](#class_attribute_names)
    - [local_class_naming](#local_class_naming)
    - [local_variable_names](#local_variable_names)
    - [method_parameter_names](#method_parameter_names)
    - [object_naming](#object_naming)
    - [form_no_dash](#form_no_dash)
  - [Formatting](#formatting)
    - [keywords_upper](#keywords_upper)
    - [line_only_punc](#line_only_punc)
    - [colon_missing_space](#colon_missing_space)
    - [contains_tab](#contains_tab)
    - [double_space](#double_space)
    - [whitespace_end](#whitespace_end)
    - [in_statement_indentation](#in_statement_indentation)
    - [indentation](#indentation)
    - [sequential_blank](#sequential_blank)
    - [start_at_tab](#start_at_tab)
    - [space_before_colon](#space_before_colon)
    - [space_before_dot](#space_before_dot)
    - [empty_line_in_statement](#empty_line_in_statement)
    - [empty_statement](#empty_statement)
  - [Other](#other)
    - [7bit_ascii](#7bit_ascii)
    - [check_variables](#check_variables)
    - [tabl_enhancement_category](#tabl_enhancement_category)
    - [ambiguous_statement](#ambiguous_statement)
    - [message_exists](#message_exists)
    - [identical_form_names](#identical_form_names)
    - [msag_consistency](#msag_consistency)
    - [parser_error](#parser_error)
    - [description_empty](#description_empty)
    - [remove_descriptions](#remove_descriptions)
    - [global_class](#global_class)
    - [begin_end_names](#begin_end_names)
    - [check_transformation_exists](#check_transformation_exists)
    - [implement_methods](#implement_methods)
    - [local_testclass_location](#local_testclass_location)
    - [main_file_contents](#main_file_contents)
    - [rfc_error_handling](#rfc_error_handling)
    - [release_idoc](#release_idoc)

## Code structure

### nesting

Checks for code exceeding a maximum nesting depth.

An exact maximum is not defined in clean abap, but I believe 5 is used in ATC. Note that in most cases you shouldn't go above 2.

https://github.com/SAP/styleguides/blob/master/clean-abap/CleanABAP.md#keep-the-nesting-depth-low

Enabled.


### definitions_top

Enforces that data and field-symbol definitions are on top of the method. While sometimes good for readability, it is an antipattern as variables should be declared inline or close to their first declaration.

Disabled.

### no_public_attributes

Checks for public attributes.

Not entirely compatible with Clean ABAP, which allows the `read-only` variant in some cases.
https://github.com/SAP/styleguides/blob/master/clean-abap/CleanABAP.md#use-read-only-sparingly

Disabled.

### unreachable code

Checks for unreachable code - lines after a `RETURN`, `EXIT` or `RAISE`. Raising exceptions might have a few false positives.

Enabled, please report false positives.

### when_others_last

Checks that `WHEN OTHERS` is the last case of a switch statement.

Enabled.

### exit_or_check

Checks for `EXIT` and `CHECK` statements outside of loops. There is no consensus on whether you should use CHECK or RETURN to exit a method if the input doesn't meet expectations.

https://github.com/SAP/styleguides/blob/master/clean-abap/CleanABAP.md#check-vs-return

Disabled.

### constructor_visibility_public

https://github.com/SAP/styleguides/blob/master/clean-abap/CleanABAP.md#if-your-global-class-is-create-private-leave-the-constructor-public

Enabled.


### short_case

Checks for `case` statements which have fewer than `length` branches. At the very least, you shouldn't have one.

`todo not sure what allow here does`

Enabled, default 2.

### max_one_statement

Checks that code only contains one statement per line.

https://github.com/SAP/styleguides/blob/master/clean-abap/CleanABAP.md#no-more-than-one-statement-per-line

Enabled.


### method_length

https://github.com/SAP/styleguides/blob/master/clean-abap/CleanABAP.md#keep-methods-small says 3-5 statements, which would raise a lot of violations. The number 25 is also used often (fits within one screen), for now I am using it a a sane max limit.

Also checks for empty methods if `errorWhenEmpty` is set to true.

Enabled.

### if_in_if

https://github.com/SAP/styleguides/blob/master/clean-abap/CleanABAP.md#keep-the-nesting-depth-low


### line_length

Enabled by default. 120 is the perscribed preferable length:

https://github.com/SAP/styleguides/blob/master/clean-abap/CleanABAP.md#stick-to-a-reasonable-line-length

## Documentation

### abapdoc

Require abapdoc comments for public methods and properties.

## Syntax/object usage

### obsolete_statement

I think it is the same thing as avoid_use. Includes `refresh`, `compute`, `add`, `subtract`, `multiply`, `move`, `divide`, `requested`.

Enabled.

### functional_writing

Checks that method calls use the functional `method()` style instead of `CALL METHOD method` if possible.

Enabled.

### avoid_use

Checks for usage of certain statements.

Currently supported:

- define (clean abap rule - no macros)
- endselect
- execSQL
- kernel call
- communication
- statics (probably a clean abap rule)

Enabled.

### breakpoint

- checks for `BREAK` and `BREAK-POINT` statements.

Should be part of clean variant, although this check could easily be merged with `avoid_use`

Enabled.

### use_new

Checks for `CREATE OBJECT` statements. You should replace these with `NEW`.

Enabled.

### preferred_compare_operators

Checks for usage of the operators listed in `badOperators`.

Enabled for comparison operators.

### mix_returning

Checks that only one returning/exporting/changing parameter is present per method in total.

https://github.com/SAP/styleguides/blob/master/clean-abap/CleanABAP.md#use-either-returning-or-exporting-or-changing-but-not-a-combination

Enabled.

### superclass_final

Checks for final classes which are inherited from. This does not pass syntax checks, but possibly makes sense to check in serialized code.

Enabled.

### cloud_types

Checks for object types incompatible with Cloud ABAP.

Types that are not

        Class
        Interface
        MessageClass
        Package
        Table
        TableType
        DataDefinition
        DataControl
        LockObject
        Transformation
        FunctionGroup
        DataElement
        Domain

Are not allowed.

`TODO make cloud ABAP variant as well`

### allowed_object_types

Allows to specify a whitelist of object types allowed in your package.

Disabled.

### inline_data_old_versions

Checks for inline data declarations in releases which are unavailable.

Enabled.

### form_tables_obsolete

Looks for `TABLES` parameters in forms. Usage of both forms and tables parameters is strongly discouraged in clean ABAP.

Enabled.

### type_form_parameters

Looks for untyped form parameters. Usage of both forms and untyped parameters is strongly discouraged in clean ABAP.

Enabled.

## Redundant code

### commented_code

Checks for commented out code. You should not generally leave commented out code so it is good that you are warned about it.

Enabled.

### empty_structure

Checks for certain empty code blocks.

Can be extended:
https://github.com/abaplint/abaplint//blob/8d29328ecc5e9c6df44b681504e6dd899abffc84/src/rules/empty_structure.ts#L16

Enabled.

### exporting

Checks for EXPORTING statements which can be omitted from method calls.

https://github.com/SAP/styleguides/blob/master/clean-abap/CleanABAP.md#omit-the-optional-keyword-exporting

Enabled.

## Naming conventions

Enables you to enforce a pattern, such as a prefix, for class, member and variable names.
Clean ABAP suggests that you eliminate prefixes, therefore this check is disabled by default.

### class_attribute_names

Class and global variables

Disabled.

### local_class_naming

Clean ABAP suggests that you eliminate prefixes, but for local classes it is very common.

This example has prefixes:
https://github.com/SAP/styleguides/blob/master/clean-abap/CleanABAP.md#call-local-test-classes-by-their-purpose

For now not enabled.

### local_variable_names

Disabled.

### method_parameter_names

Disabled.

### object_naming

Allows to define prefixes for object types. This differs per project.

Disabled.

### form_no_dash

Checks for a dash `-` in form names. Usage of dashes in names is heavily discouraged.

Enabled.

## Formatting

Warning:

Enabling some of the formatting checks might lead to a lot of violations, as old editors reformat class headers and pretty printer only fixes most punctuation issues.
Some of them can be draconic to maintain without proper tooling to fix the formatting, which might improve in the future.

The clean code config enables by default the rules which shouldn't be common enough to cause too many violations.

Enable more of them yourself according to your preferred conventions.

### keywords_upper

Checks that keywords are in uppercase. Parameters allow to skip certain parts of code such as class definitions, which can be reformatted by SE80.

### line_only_punc

Checks for lines containing only . or ).

### colon_missing_space

Checks for a missing space after a colon in chained statements. This is good indentation practice.

Example:

```abap
" incorrect
WRITE:`abc`.

"correct
WRITE: `abc`.
```

### contains_tab

Checks for tabs in your code. Enable if you want to enforce usage of spaces.

### double_space

I think this ensures that there is a `single` space after certain keywords and parentheses. This is good indentation practice.

List of keywords can be extended, see
https://github.com/abaplint/abaplint//blob/ba4c6f8d03eb8d1a31c277d06c9d9cb9e7ad86b8/src/rules/whitespace/double_space.ts#L42


### whitespace_end

Checks for whitespace at the end of a line. This is good indentation practice, may lead to many errors.

### in_statement_indentation

Checks alignment within block statement declarations which span multiple lines, such as multiple conditions in IF statements.

Example violation:
``` abap
IF 1 = 1 AND
           2 = 2.
ENDIF.
```

### indentation

Check indentation of nested blocks. Clean code should definitely be well indented.

Example violation:

```abap
    IF 1 = 2.
  IF 3 = 4.
  ENDIF.
    ENDIF.
```

Enabled.

### sequential_blank

Checks for multiple successive blank lines in code. The maximium allowed number is configurable.

Enabled.

### start_at_tab

Ensures code starts at tabstop positions. Enable if you want to enforce tabs.

### space_before_colon

Checks that there are no spaces in front of colons in chained statements.

Example violation:
`write : 'a'`

### space_before_dot

Checks for spaces before dots like `this .` These are quite common in class definitions generated by SE80.

### empty_line_in_statement

Checks for empty lines in statements. Example violation:

```abap
DATA(x) = y

.
```

The `allowChained` parameter can be used to disable the check in chained statements.


This should be a very rare formatting issue.

Enabled for non-chained statements.

### empty_statement

Checks for empty statements in your code. An empty statement is a single dot `.`.

This should be a very rare formatting issue.

Enabled.

## Other

### 7bit_ascii

Checks that your code contains only characters from the 7bit ASCII set. This practice should not be required on modern systems with unicode support.

Disabled.


### check_variables

Enables variable analysis (experimental).

Enabled.

### tabl_enhancement_category

Checks that tables do not have the enhancement category *not classified*.

Enabled.

### ambiguous_statement

In some cases, the abaplint parser cannot tell whether a delete is performed on a database table or an internal table. Enabling the rule will force you to use more explicit syntax.

Enabled.

### message_exists

Checks that a message class and id exists.

Enabled.

### identical_form_names

Checks for identically named forms. Form usage is discouraged in general.

Enabled.


### msag_consistency

Checks serialized message classes.

- id is 3 digit
- text exists

Enabled.

### parser_error

Report abaplint failures. You should log these as issues on https://github.com/abaplint/abaplint/issues so that they can be fixed.

Enabled

### description_empty

Checks for empty descriptions in the abapGit xml metadata. While not part of abap, this helps ensure the consistency of your serialized files.

Enabled.

### remove_descriptions

Ensures you have no descriptions in your metadata. This relates to methods, parameters, etc. For class descriptions, see [description_empty](#description_empty).
The descriptions originate either from the form-based SE80 editor or if you use `shorttext synchronized` in abapdoc.
The abaplint philosophy is that you should just use `"!` because `shorttext synchronized` hurts readability.

Disabled because SAP wants you to use shorttext synchronized (although I agree with the readability issue).

### global_class

Mostly checks abapGit metadata for class names. The situations checked for are caused by code which can't be activated, but the rule is enabled for some extra validation.

### begin_end_names

Checks that names in the `begin of ...` and `end of ...` match. Code violating this rule is invalid.

Enabled.

### check_transformation_exists

Validates that transformations called in your code exist.

Enabled.

### implement_methods

Looks for abstract methods which are not yet implemented. Code violating this rule is invalid.

Enabled.

### local_testclass_location

Validates that test classes are placed within the test include.

Enabled.

### main_file_contents

Validations related to report definitions.

- a report must have a name
- a report must begin with `REPORT`
- report name and filename must match

Enabled.


### rfc_error_handling

Checks that exceptions 'resource_failure' 'system_failure' and 'communication_failure' are handled in RFC calls.

Correct handling example:

```abap
CALL FUNCTION 'FOO' DESTINATION 'BAR'
      EXCEPTIONS
        system_failure        = 1 MESSAGE lv_msg
        communication_failure = 2 MESSAGE lv_msg
        resource_failure      = 3.`
````

### release_idoc

Checks idoc types and segments are set to status released