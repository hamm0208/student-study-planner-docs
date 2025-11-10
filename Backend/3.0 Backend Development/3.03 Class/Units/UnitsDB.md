# UnitDB

`UnitDB` is a static utility class to interact with the Units API. It provides the crucial methods to fetch, create, update and delete unit records from the backend.

---

## Class Directory

```directory
src/app/class/
	├── Unit/
		├── UnitDB.js
```

## Methods

### FetchUnits

This method is used to specifically fetch the units from the server with optional query parameters.

```js
UnitDB.FetchUnits(params)
```

#### Parameters

|Name|Type|Optional|Description|Example|
|---|---|---|---|---|
|params|Object|Yes (Returns all)|Query parameters for filtering, sorting, selecting and excluding data.|Below:|

Params:

|Name|Optional|Type|Description|Example|
|---|---|---|---|---|
|**code**|Yes|`string`|Unit code for filtering specific units.|`"MATH101"`|
|**name**|Yes|`string`|The name of the unit.|`"Introduction to Calculus"`|
|**cp**|Yes|`float`|Credit points of the unit.|`6.0`|
|**availability**|Yes|`string`|Availability status of the unit.|`"published"`|
|**order_by**|Yes|`Array<Object>`|Sorting rules<br>(column + order).|`[{ "column": "UnitCode", "ascending": true }]`|
|**return**|Yes|`Array<string>`|Fields to return in the response.|`["UnitCode", "Name", "CreditPoints"]`|
|**exclude**|Yes|`Object`|Exclude certain values from results (per fields).|`{ UnitCode: ["MATH101"], Name: ["Calculus"] }`|

```js
{
  code: "MATH101",
  name: "Introduction to Calculus",
  cp: 6.0,
  availability: "published",
  return: ["UnitCode", "Name", "CreditPoints", "Availability"],
  order_by: [
    { column: "UnitCode", ascending: true }
  ],
  exclude: {
    UnitCode: ["MATH101"],
    Name: ["Advanced Topics"],
    CreditPoints: [12.5],
    Availability: ["unpublished"]
  }
}
```

#### Notes:

- For return, the field names have to be exactly the same as the ones in the DB.
- For order_by, the column names have to be exactly the same as the ones in the DB.
- For exclude, the object's properties names have to be exactly the same as the ones in DB.

#### Returns

|Field|Type|Description|Example Value|
|---|---|---|---|
|`success`|boolean|Indicates whether the request was successful or not.|`true` / `false`|
|`message`|string|Human-readable message explaining the result (on error).|`"Failed to fetch data"`|
|`data`|array|Array of `Unit` instances.|`[Unit, Unit, Unit]`|
|`pagination`|object|Pagination information (if applicable).|`{ page: 1, limit: 10, total: 50 }`|

---

## AddUnit

Adds a new unit to the server.

```js
UnitDB.AddUnit(unit)
```

#### Parameters

|Name|Type|Description|Optional|Example|
|---|---|---|---|---|
|unit|Object|A unit object<br>to be added|No|`{ code: "MATH101", name: "Calculus", cp: 6.0, availability: "published" }`|

Unit Object Properties:

|Name|Type|Description|Example|
|---|---|---|---|
|**code**|`string`|Unit code (e.g., "COS20004").|`"MATH101"`|
|**name**|`string`|Unit name.|`"Introduction to Calculus"`|
|**cp**|`float`|Credit points (e.g., 12.5).|`6.0`|
|**availability**|`string`|Availability status (e.g., "published").|`"published"`|

#### Returns

|Field|Type|Description|Example Value|
|---|---|---|---|
|`success`|boolean|Indicates whether the request was successful or not.|`true` / `false`|
|`message`|string|Human-readable message explaining the result.|`"Unit added successfully"` / `"Failed to add unit"`|
|`unit`|object|The unit that was created (only present on success).|`{ code: "MATH101", name: "Calculus", ... }`|

---

## UpdateUnit

Updates an existing unit on the server.

```js
UnitDB.UpdateUnit(unit)
```

#### Parameters

|Name|Type|Description|Optional|Example|
|---|---|---|---|---|
|unit|Object|The unit object to be updated. Contains new values and original_code to identify the unit.|No|`{ code: "MATH102", name: "Advanced Calculus", cp: 6.0, availability: "published", original_code: "MATH101" }`|

Unit Object Properties:

|Name|Type|Description|Example|
|---|---|---|---|
|**code**|`string`|New unit code.|`"MATH102"`|
|**name**|`string`|Unit name.|`"Advanced Calculus"`|
|**cp**|`float`|Credit points.|`6.0`|
|**availability**|`string`|Availability status.|`"published"`|
|**original_code**|`string`|Original unit code to identify the unit.|`"MATH101"`|

#### Returns

|Field|Type|Description|Example Value|
|---|---|---|---|
|`success`|boolean|Indicates whether the request was successful or not.|`true` / `false`|
|`message`|string|Human-readable message explaining the result.|`"Unit updated successfully"` / `"Failed to update unit"`|
|`unit`|object|The unit that was updated (only present on success).|`{ code: "MATH102", name: "Advanced Calculus", ... }`|

---

## DeleteUnit

Deletes an existing unit from the server.

```js
UnitDB.DeleteUnit(unit_code)
```

#### Parameters

|Name|Type|Description|Optional|Example|
|---|---|---|---|---|
|unit_code|`string`|The unit code of the unit to be deleted.|No|`"MATH101"`|

#### Returns

|Field|Type|Description|Example Value|
|---|---|---|---|
|`success`|boolean|Indicates whether the request was successful or not.|`true` / `false`|
|`message`|string|Human-readable message explaining the result.|`"Unit deleted successfully"` / `"Failed to delete unit"`|

---

### Example Usage

```js
import UnitDB from './UnitDB';

// Fetch units
const units = await UnitDB.FetchUnits({ 
  order_by: [{ column: "UnitCode", ascending: true }]  
});

// Add a unit
const addUnit = await UnitDB.AddUnit({
  code: "MATH101",
  name: "Introduction to Calculus",
  cp: 6.0,
  availability: "published"
});

// Update a unit
const updateUnit = await UnitDB.UpdateUnit({
  code: "MATH102",
  name: "Advanced Calculus", 
  cp: 6.0,
  availability: "published",
  original_code: "MATH101"
});

// Delete a unit
const deleteUnit = await UnitDB.DeleteUnit("MATH101");
```

---

### Notes

- All methods are asynchronous and return Promises.
- Error handling is performed internally and errors are logged to the console.
- The API endpoint is determined by the `NEXT_PUBLIC_SERVER_URL` environment variable.
- FetchUnits automatically fetches related requisites and offered terms data.
- Unit instances are created with requisites and offered_terms populated from related tables.

```javascript
export default UnitDB;
```