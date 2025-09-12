## Overview

The `Term` class class represents the Terms of the Study Planner, which represents a fix study period for the students to register in, for units that are available in specific terms.

## Constructor
```js
new Terms({ id = null, name, year, month, semtype, status })
```
## Parameters
| Name        | Type      | Description                                                                  |
| ----------- | --------- | ---------------------------------------------------------------------------- |
| **id**      | `number`  | The unique identifier for the Term.                                          |
| **name**    | `string`  | The name of the Term.                                                        |
| **month**   | `string`  | The month that the Term will be available by.                                |
| **semtype** | `boolean` | The type of semester for the term (`"Long Semester"`, `"Short."`)            |
| **status**  | `boolean` | The current status of the term (`"Published"`, `"Unpublished."`,`"Private"`) |

## Properties
| Name        | Type      | Description                                    |
| ----------- | --------- | ---------------------------------------------- |
| **id**      | `number`  | Gets or sets the term unique identifier.       |
| **name**    | `string`  | Gets or sets of the name of the term.          |
| **month**   | `string`  | Gets or sets of the month of the term.         |
| **semtype** | `boolean` | Gets or sets of the semester type of the term. |
| **status**  | `boolean` | Gets or sets of the terms status               |
## Example Usage

```js
Hello heloo 1 2 3
```
## Getters and Setters


## Export



