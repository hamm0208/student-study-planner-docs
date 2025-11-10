# CourseIntakeDB

The `CourseIntakeDB` class provides static methods for interacting with the `Course Intake` database via API calls. It handles fetching, adding, updating, deleting, and batch updating `Course Intake` records in the study planner system.

---

## Class Directory

```js
src/app/class/
    ├── CourseIntake/
        ├── CourseIntakeDB.js
```

---

## Methods

### `static async FetchCourseIntakes(params)`
Fetches a list of `Course Intake` records from the server, with optional query parameters for filtering, ordering, and field selection.

#### Parameters

| Name     | Type     | Description                                                     |
| -------- | -------- | --------------------------------------------------------------- |
| `params` | `object` | Query parameters for filtering, ordering, and selecting fields. |

#### Returns

- An object containing:
    - `success: `boolean`
    - `data`: `CourseIntake` (array of `Course Intake` instances)
    - `message`: `string` (on error)

---

### static async AddCourseIntake(intake)

Adds a new `Course Intake` record to the server.

#### Parameters

| Name     | Type     | Description                      |
| -------- | -------- | -------------------------------- |
| `intake` | `object` | The `Course Intake` data to add. |

#### Returns

- An object containing:
    - `success`: `boolean`
    - message: `string`
    - `intake`: `object` (added intake, if successful)

---

### static async UpdateCourseIntake(intake)

Updates an existing `Course Intake` record on the server.

#### Parameters

| Name     | Type     | Description                       |
| -------- | -------- | --------------------------------- |
| `intake` | `object` | The updated `Course Intake` data. |

#### Returns

- An object containing:
    - `success`: `boolean`
    - `message]`: `string`
    - `intake`: `object` (updated intake, if successful)

---

### static async DeleteCourseIntake(ids)

Deletes one or more `Course Intake` records from the server by their IDs.

#### Parameters

| Name  | Type       | Description                    |
| ----- | ---------- | ------------------------------ |
| `ids` | `number[]` | Array of intake IDs to delete. |

#### Returns

- An object containing:
    - `success`: `boolean`
    - `message`: `string`

---

### static async BatchUpdateIntakes(intakes)

Updates multiple `Course Intake` records in a single transaction.
#### Parameters

| Name      | Type       | Description                                 |
| --------- | ---------- | ------------------------------------------- |
| `intakes` | `object[]` | Array of `Course Intake` objects to update. |

#### Returns

- An object containing:
    - `success`: `boolean`
    - `message`: `string`

---

## Example Usage

```js
import CourseIntakeDB from `CourseIntakeDB`;

// Fetch course intakes
const result = await CourseIntakeDB.FetchCourseIntakes({ status: 'Open' });
if (result.success) {
    console.log(result.data); // Array of `Course Intake` instances
}

// Add a course intake
const addResult = await CourseIntakeDB.AddCourseIntake({
    Status: 'Open',
    TermID: 2025,
    MajorID: 10
});

// Update a course intake
const updateResult = await CourseIntakeDB.UpdateCourseIntake({
    ID: 1,
    Status: 'Closed',
    TermID: 2025,
    MajorID: 10
});

// Delete course intakes
await CourseIntakeDB.DeleteCourseIntake([1, 2, 3]);

// Batch update intakes
await CourseIntakeDB.BatchUpdateIntakes([
    { ID: 1, Status: 'Closed', TermID: 2025, MajorID: 10 },
    { ID: 2, Status: 'Open', TermID: 2026, MajorID: 11 }
]);
```

---

## Export

The class is exported as the default export from the module.
```js
export default CourseIntakeDB;
```