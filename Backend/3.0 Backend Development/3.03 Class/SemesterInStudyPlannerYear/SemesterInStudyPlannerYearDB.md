## Overview

`SemesterInStudyPlannerYearDB` is a static utility class for interacting with the Semester In Study Planner Year API. It provides methods to fetch, add, update, and delete semester records associated with a master study planner.

---

## Methods

### 1. FetchSemesterInStudyPlannerYears

Fetches semesters from the server with optional query parameters.

```js
SemesterInStudyPlannerYearDB.FetchSemesterInStudyPlannerYears(params)
```

#### Parameters
| Name   | Type   | Description                                                  | Optional                  | Example |
| ------ | ------ | ------------------------------------------------------------ | ------------------------- | ------- |
| params | Object | Query parameters for filtering, sorting, and selecting data. | Yes (Return all if empty) |         |
- **order_by**: Array of objects specifying columns and sort order.
- **return**: Array of strings specifying which fields to return.
- **exclude**: Array of strings specifying which fields to exclude.
#### Params
| Name                 | Optional | Type                   | Description                                                      | Example                                                   |
| -------------------- | -------- | ---------------------- | ---------------------------------------------------------------- | --------------------------------------------------------- |
| **id**               | Yes      | `number` \| `null`     | Unique identifier for a specific master study planner. Optional. | `123`                                                     |
| **course_intake_id** | Yes      | `number` \| `number[]` | One or multiple course intake IDs to filter by.                  | `1` or `[3, 4]`                                           |
| **status**           | Yes      | `string`               | Status of the master study planner.                              | `"complete"`                                              |
| **return**           | Yes      | `string[]`             | List of attributes to include in the response.                   | `["ID", "Status"]`                                        |
| **order_by**         | Yes      | `Array<Object>`        | Sorting rules (column + order).                                  | `[ { "column": "ID", "ascending": true } ]`               |
| **exclude**          | Yes      | `Object`               | Exclude certain values from results (per field).                 | `{ ID: [1,2], CourseIntakeID: [1,2], Status: ["Empty"] }` |
```params:
{
  id: 123,
  course_intake_id: 1 OR [3, 4],
  status: "complete",
  return: ["ID", "Status"], ... (All of the columns in the DB acceptable)
  order_by: [
	  { column: "ID", ascending: true },
	  ... (All of the columns in the DB acceptable) 
  ],
  exclude: {
    ID: [1, 2], //exclude where ID is 1 and 2
    ... (All of the columns in the DB acceptable)
  }
}
```
#### Notes:
- For return, the name have to be exactly the same as the one in DB
- For order_by, the column's name have to be exactly the same as the one in DB
- For exclude, the object's properties name have to be exactly the same as the one in DB
#### Returns

- Array of `SemesterInStudyPlannerYear` instances.

---

### 2. AddSemesterInStudyPlannerYear

Adds a new semester to the server.

```js
SemesterInStudyPlannerYearDB.AddSemesterInStudyPlannerYear(semester)
```

#### Parameters

| Name     | Type                       | Description                      | Optional | Example                                                                   |
| -------- | -------------------------- | -------------------------------- | -------- | ------------------------------------------------------------------------- |
| semester | SemesterInStudyPlannerYear | The semester object to be added. | No       | `{ master_study_planner_id: 101, year: 2025, sem_type: 'Long Semester' }` |

#### Return(s) Object:

| Field     | Type                 | Description                                                                                                            | Example                                                                                             |
| --------- | -------------------- | ---------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| `success` | `boolean`            | Indicates whether the request was successful or not.                                                                   | `true` or `false`                                                                                   |
| `message` | `string`             | Provides a human-readable message about the result of the operation.                                                   | `"Semesters added successfully"` `"Cannot add more Long Semesters. Maximum of 2 per year allowed."` |
| `data`    | `array of objects`   | Contains the newly created semester records. Each object includes `ID`, `MasterStudyPlannerID`, `Year`, and `SemType`. | `[ { ID: 1, MasterStudyPlannerID: 123, Year: 2025, SemType: "Long Semester" } ]`                    |
| `status`  | `number` (HTTP code) | The HTTP status code returned with the response.                                                                       | `200` for success, `400` for validation errors, `500` for server errors                             |

---

### 3. UpdateSemesterInStudyPlannerYear

Updates an existing semester on the server.

```js
SemesterInStudyPlannerYearDB.UpdateSemesterInStudyPlannerYear(semester)
```

#### Parameters

| Name     | Type                       | Description                          | Optional | Example                                  |
|----------|----------------------------|--------------------------------------|----------|------------------------------------------|
| semester | SemesterInStudyPlannerYear | The semester object to be updated.   | No       | `{ id: 1, master_study_planner_id: 101, year: 2025, sem_type: 'Short Semester' }` |

#### Returns
| Field     | Description                                                               |
| --------- | ------------------------------------------------------------------------- |
| `success` | A boolean indicating if the operation was successful (`true` or `false`). |
| `message` | A human-readable message describing the result of the operation.          |
| `data`    | The actual payload returned from the server, e.g., the updated semester.  |

---
### 4. DeleteSemesterInStudyPlannerYear

Deletes one or more semesters from the server by their IDs.

```js
SemesterInStudyPlannerYearDB.DeleteSemesterInStudyPlannerYear(ids)
```

#### Parameters
| Name | Type  | Description                      | Optional | Example     |
| ---- | ----- | -------------------------------- | -------- | ----------- |
| ids  | Array | Array of semester IDs to delete. | No       | `[1, 2, 3]` |
#### Returns
- Object containing `success`, `message`, and `data`.

---

## Example Usage

```js
import SemesterInStudyPlannerYearDB from './SemesterInStudyPlannerYearDB';

// Fetch semesters
const semesters = await SemesterInStudyPlannerYearDB.FetchSemesterInStudyPlannerYears({ order_by: [{ column: 'Year', ascending: true }] });

// Add a semester
const addResult = await SemesterInStudyPlannerYearDB.AddSemesterInStudyPlannerYear({ master_study_planner_id: 101, year: 2025, sem_type: 'Long Semester' });

// Update a semester
const updateResult = await SemesterInStudyPlannerYearDB.UpdateSemesterInStudyPlannerYear({ id: 1, master_study_planner_id: 101, year: 2025, sem_type: 'Short Semester' });

// Delete semesters
const deleteResult = await SemesterInStudyPlannerYearDB.DeleteSemesterInStudyPlannerYear([1, 2, 3]);
```

---
## Notes

- All methods are asynchronous and return Promises.
- Error handling is performed internally and errors are logged to the console.
- The API endpoint is determined by the `NEXT_PUBLIC_SERVER_URL` environment variable.****