# Unit

The `Unit` class represents academic units/courses in the Study Planner, which contains information about course codes, names, availability, prerequisites, credit points, and the terms when they are offered to students.


## Class Directory

```directory
src/app/class/
	├── Unit/
		├── unit.js
```

## Constructor

```js
new Unit({ unit_code, name, availability, requisites, credit_points, offered_terms })
```

## Parameters

|Name|Type|Description|
|---|---|---|
|**unit_code**|`string`|The unique identifier/code for the unit.|
|**name**|`string`|The full name of the unit.|
|**availability**|`string` \| `boolean`|The current availability status of the unit.|
|**requisites**|`string` \| `object` \| `array` \| `null`|The prerequisites or requirements for the unit (default: `null`).|
|**credit_points**|`number`|The number of credit points the unit is worth.|
|**offered_terms**|`array`|The terms/semesters when the unit is offered (default: `[]`).|

## Properties

|Name|Type|Description|
|---|---|---|
|**unit_code**|`string`|Gets or sets the unit's unique identifier/code.|
|**name**|`string`|Gets or sets the unit's full name.|
|**availability**|`string` \| `boolean`|Gets or sets the unit's availability status.|
|**requisites**|`string` \| `object` \| `array` \| `null`|Gets or sets the unit's prerequisites/requirements.|
|**credit_points**|`number`|Gets or sets the unit's credit points value.|
|**offered_terms**|`array`|Gets or sets the terms when the unit is offered.|

## Example Usage

```js
import Unit from './unit';
const unit = new Unit({
	unit_code: 'MATH101',
	name: 'Introduction to Calculus',
	availability: true,
	requisites: null,
	credit_points: 6,
	offered_terms: ['Semester 1', 'Semester 2']
});
console.log(unit.unit_code); // COS20006
console.log(unit.name); // Comp Sci Subject 101
console.log(unit.availability); // true
console.log(unit.requisites); // null
console.log(unit.credit_points); // 6
console.log(unit.offered_terms); // ['Semester 1', 'Semester 2']
```

## Getters and Setters

- `unit_code`: Get or set the unit's code/identifier.
- `name`: Get or set the unit's full name.
- `availability`: Get or set the unit's availability status.
- `requisites`: Get or set the unit's prerequisites or requirements.
- `credit_points`: Get or set the unit's credit points value.
- `offered_terms`: Get or set the terms when the unit is offered.

## Export

The class is exported as the default export from the module.

```js
export default Unit;
```