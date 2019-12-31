# Rule descriptions
- [Rule descriptions](#rule-descriptions)
  - [Code structure](#code-structure)
    - [nesting](#nesting)
    - [definitions_top](#definitionstop)
    - [no_public_attributes](#nopublicattributes)
    - [unreachable code](#unreachable-code)
    - [when_others_last](#whenotherslast)
    - [exit_or_check](#exitorcheck)
    - [constructor_visibility_public](#constructorvisibilitypublic)
    - [short_case](#shortcase)
    - [max_one_statement](#maxonestatement)
    - [method_length](#methodlength)
    - [if_in_if](#ifinif)
    - [line_length](#linelength)
    - [prefer_returning_to_exporting](#preferreturningtoexporting)
  - [Documentation](#documentation)
    - [abapdoc](#abapdoc)
    - [check_comments](#checkcomments)
  - [Syntax/object usage](#syntaxobject-usage)
    - [obsolete_statement](#obsoletestatement)
    - [functional_writing](#functionalwriting)
    - [avoid_use](#avoiduse)
    - [breakpoint](#breakpoint)
    - [use_new](#usenew)
    - [preferred_compare_operators](#preferredcompareoperators)
    - [mix_returning](#mixreturning)
    - [superclass_final](#superclassfinal)
    - [cloud_types](#cloudtypes)
    - [allowed_object_types](#allowedobjecttypes)
    - [inline_data_old_versions](#inlinedataoldversions)
    - [form_tables_obsolete](#formtablesobsolete)
    - [type_form_parameters](#typeformparameters)
    - [chain_mainly_declarations](#chainmainlydeclarations)
    - [fully_type_constants](#fullytypeconstants)
  - [Redundant code](#redundant-code)
    - [commented_code](#commentedcode)
    - [empty_structure](#emptystructure)
    - [exporting](#exporting)
  - [Naming conventions](#naming-conventions)
    - [class_attribute_names](#classattributenames)
    - [local_class_naming](#localclassnaming)
    - [selection_screen_naming](#selectionscreennaming)
    - [local_variable_names](#localvariablenames)
    - [method_parameter_names](#methodparameternames)
    - [object_naming](#objectnaming)
    - [form_no_dash](#formnodash)
    - [allowed_object_naming](#allowedobjectnaming)
  - [Formatting](#formatting)
    - [keyword_case](#keywordcase)
    - [line_only_punc](#lineonlypunc)
    - [colon_missing_space](#colonmissingspace)
    - [contains_tab](#containstab)
    - [double_space](#doublespace)
    - [whitespace_end](#whitespaceend)
    - [in_statement_indentation](#instatementindentation)
    - [indentation](#indentation)
    - [sequential_blank](#sequentialblank)
    - [start_at_tab](#startattab)
    - [space_before_colon](#spacebeforecolon)
    - [space_before_dot](#spacebeforedot)
    - [empty_line_in_statement](#emptylineinstatement)
    - [empty_statement](#emptystatement)
    - [keep_single_parameter_on_one_line](#keepsingleparameterononeline)
  - [Other](#other)
    - [7bit_ascii](#7bitascii)
    - [check_syntax](#checksyntax)
    - [tabl_enhancement_category](#tablenhancementcategory)
    - [ambiguous_statement](#ambiguousstatement)
    - [message_exists](#messageexists)
    - [identical_form_names](#identicalformnames)
    - [msag_consistency](#msagconsistency)
    - [parser_error](#parsererror)
    - [description_empty](#descriptionempty)
    - [remove_descriptions](#removedescriptions)
    - [global_class](#globalclass)
    - [begin_end_names](#beginendnames)
    - [check_transformation_exists](#checktransformationexists)
    - [implement_methods](#implementmethods)
    - [local_testclass_location](#localtestclasslocation)
    - [main_file_contents](#mainfilecontents)
    - [rfc_error_handling](#rfcerrorhandling)
    - [release_idoc](#releaseidoc)
    - [check_abstract](#checkabstract)
    - [check_text_elements](#checktextelements)

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

Enabled (read-only is allowed).

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

Can be configured to ignore test classes.

Also checks for empty methods if `errorWhenEmpty` is set to true.

Enabled.

### if_in_if

https://github.com/SAP/styleguides/blob/master/clean-abap/CleanABAP.md#keep-the-nesting-depth-low


### line_length

Enabled by default. 120 is the perscribed preferable length:

https://github.com/SAP/styleguides/blob/master/clean-abap/CleanABAP.md#stick-to-a-reasonable-line-length

### prefer_returning_to_exporting

Checks for `exporting` parameters which can be turned into `returning`.

https://github.com/SAP/styleguides/blob/master/clean-abap/CleanABAP.md#prefer-returning-to-exporting

Enabled.

## Documentation

### abapdoc

Require abapdoc comments for public methods and properties.

### check_comments

Can be used to disallow end of line comments using the parameter `allowEndOfLine`.

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

### chain_mainly_declarations

Restricts the use of chaining to declarations.

https://docs.abapopenchecks.org/checks/23/

### fully_type_constants

Checks that constants are fully typed.

```
" incorrectly typed - these are implicitly `type c length 1`
CONSTANTS: tested_name1 VALUE `blah`.
CONSTANTS: tested_name2 VALUE 'blah'.

CONSTANTS: tested_name3 VALUE 1234.

" correctly typed
CONSTANTS: tested_name4 type string VALUE 'blah'.
CONSTANTS: tested_name5 type i VALUE 1234.
```

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

### selection_screen_naming

Enables you to enforce a pattern, such as a prefix, for selection screen `paramters` and `select-options`.

Clean ABAP suggests that you eliminate prefixes, therefore this check is disabled by default.

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

### allowed_object_naming

Checks validity of object names (for example invalid characters, max length)

Enabled.

## Formatting

Warning:

Enabling some of the formatting checks might lead to a lot of violations, as old editors reformat class headers and pretty printer only fixes most punctuation issues.
Some of them can be draconic to maintain without proper tooling to fix the formatting, which might improve in the future.

The clean code config enables by default the rules which shouldn't be common enough to cause too many violations.

Enable more of them yourself according to your preferred conventions.

### keyword_case

Checks that keywords are in a consistent case specified in `style`. Other parameters allow to skip certain parts of code such as class definitions, which can be reformatted by SE80.

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

### keep_single_parameter_on_one_line

Checks for single parameter method calls which are not in a single line.

The paramter `length` can be used to suppress the warning for long lines.

Good example

```
cl_foo=>bar( x = 5 ).
```

Bad example

```
cl_foo=>bar(
    x = 5 ).
```

## Other

### 7bit_ascii

Checks that your code contains only characters from the 7bit ASCII set. This practice should not be required on modern systems with unicode support.

Disabled.


### check_syntax

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
        resource_failure      = 3.
```

### release_idoc

Checks idoc types and segments are set to status released

### check_abstract

Checks that

- no class is abstract + final
- non-abstract classes do not contain abstract methods

Enabled.

### check_text_elements

Checks existence of text elements and they match their string literal values.

Enabled.