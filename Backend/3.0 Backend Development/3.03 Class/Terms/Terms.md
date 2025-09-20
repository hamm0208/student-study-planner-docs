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
import Terms from './term';

const terms = new term({
	id: 1,
	name: '2025_FEB',
	month: 'February',
	semtype: 'Long Semester',
	status: 'Published'
});

console.log(terms.id); //1
console.log(terms.name); //2025_FEB
console.log(terms.month); //February
console.log(terms.semtype); //Long Semester 
console.log(terms.status); //Published
```
## Getters and Setters
- `id` : Get or set the term's ID.
- `name`: Get or set the term's Name.
- `month`: Get or set the term's Month.
- `semtype`: Get or set the term's Semester Type.
- `status`: Get or set the term's current Status.

## Export

The class is exported as the default export from the module.
```js
export default Terms;
```


