## Overview
`TermsDB` is a static utility class to interact with the Terms API. It provides the crucial methods to fetch, create, update and delete terms records from the backend. 

--- 

## Methods 

### 1. FetchTerms
This method is used to specifically fetch the terms from the server with optional query parameters. 

```js
termDB.FetchTerms(params)
```

#### Parameters
| Name   | Type   | Optional          | Description                                                            | Example |
| ------ | ------ | ----------------- | ---------------------------------------------------------------------- | ------- |
| params | Object | Yes (Returns all) | Query parameters for filtering, sorting, selecting and excluding data. | Below:  |

Params:

| Name         | Optional | Type               | Description                                                      | Example                                                   |
| ------------ | -------- | ------------------ | ---------------------------------------------------------------- | --------------------------------------------------------- |
| **id**       | Yes      | `number` \| `null` | Unique identifier for a specific master study planner. Optional. | `67`                                                      |
| **name**     | Yes      | `string`           | The name of the terms.                                           | '2025_FEB'                                                |
| **month**    | Yes      | `string`           | The month of the terms.                                          | 'February'                                                |
| **semtype**  | Yes      | `boolean[]`        | The type of semester the term is.                                | 'Long Semester'                                           |
| **status**   | Yes      | `boolean[]`        | The current status of the term.                                  | 'Published'                                               |
| **order_by** | Yes      | `Array<Object>`    | Sorting rules<br>(column + order).                               | [ { `"column": "ID","ascending" true`}]                   |
| **exclude**  | Yes      | `Object`           | Exclude certain values from results (per fields)                 | { `ID: [1, 2],``CourseIntakeID: [1,2], Status:["Empty"]`' |

```js
{
id: 67,
name:'2025_FEB',
month:'February',
semtype:'Long Semester',
status: "Published"
return: ["ID", "Month", "Semester Type","Published" ]
order_by: [
	{column: "ID", ascending: true}
],
exclude:{
	ID: [67],
	month: [2],
	semtype: [Published],
	status: [Long Semester]
	}
}
```
#### Notes:
- For return, the name have to be exactly the same as the one in the DB.
- For order_by, the column's have to be exactly the same as the one in the DB.
- For exclude, the object's properties name have to be exactly the same as the one in DB.

#### Returns
- Array of `Terms` instances.

---

## 2. AddTerms

Adds a new master study planner to the server. 
```js
Terms.AddTerms(term_id)
```

#### Parameters

| Name    | Type  | Description                      | Optional | Example                                 |
| ------- | ----- | -------------------------------- | -------- | --------------------------------------- |
| term_id | Terms | A term_id object <br>to be added | No       | '`{term_id: 12,`<br>`status: 'Empty'`}' |
#### Returns
| Field     | Type    | Description                                                                                                                | Example Value                                                                                                      |
| --------- | ------- | -------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| `success` | boolean | Indicates whether the request was successful or not.                                                                       | `true` / `false`                                                                                                   |
| `message` | string  | Human-readable message explaining the result.                                                                              | `"Term added successfully"` / `"Failed to add term"`                                                               |
| `data`    | array   | Array of newly created Terms (only present on success). Each object contains `ID`, `Name`, `Month`, `SemType`and `Status`. | `[{"ID": 1,<br>`"Name": 2025_JUN,<br>`"Month": June"`,<br>`"Semtype":"Short Semester"`<br>`"Status": "Complete"}]` |
| `ids`     | array   | Array of IDs of the newly created planners (only present on success).                                                      | `[1, 2, 3]`                                                                                                        |
| `status`  | number  | HTTP status code for the response                                                                                          | `400` / `500`                                                                                                      |

---

## 3 UpdateTerms
Updates an existing Term on the server. 

```js
termsDB.UpdateTerms(term)
```

#### Parameters 
| Name | Type  | Description                                                                                                         | Optional | Example                                                                                       |
| ---- | ----- | ------------------------------------------------------------------------------------------------------------------- | -------- | --------------------------------------------------------------------------------------------- |
| term | Terms | The term object to be updated. Only certain variables can be updated ('`Name'`, `'Month'`, `'SemType'`, `"Status"`) | No       | `{ id: 3, Name: 2026_MAR, Month: "March", Semtype: "Long Semester" ,status: 'Unpublished'  }` |

#### Returns 

| Field     | Type    | Description                                                                                                                          | Example Value                                                                                  |
| --------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------- |
| `success` | boolean | Indicates whether the request was successful or not.                                                                                 | `true` / `false`                                                                               |
| `message` | string  | Human-readable message explaining the result.                                                                                        | `"Term has been editted successfully"` / `"Failed to edit the term"`                           |
| `term`    | object  | The master study planner that was created (only present on success). Contains ``ID``, ``Name``, ``Month``, ``Semtype``,and `Status`. | ``{ id: 3, Name: 2028_MAR, Month: "March", Semtype: "Short Semester" ,status: 'Published'  }`` |

--- 
### Example Usage
```js
import TermDB from '.termDB';

//Fetch term
const term = await TermsDB.FetchTerms({ order_by: [{ column: "ID", ascending: true}]  });

//Add a term
const addTerm = await TermDB.AddTerm({
term_id : 100, status: 'Published'});

//Update a term
const UpdateTerm = await TermDB.UpdateTerm({
term_id: 15, status: 'Unpublished'
});
```

---

### Notes

- All methods are asynchronous and return Promises.
- Error handling is performed internally and errors are logged to the console. 
- The API endpoint is determined by the `NEXT_PUBLIC_SERVER_URL`

