# StudyPlanner
The `StudyPlanner` class serves as the core model for the master study planner view page. It manages all planner logic, including adding and removing unit rows and semesters, calculating next semester intakes, and detecting unit conflicts. The class also handles backend-related calculations and state updates to ensure the planner remains accurate and up-to-date.

---
## Class Directory
```directory
src/app/class/
	├── StudyPlanner/
		├── StudyPlanner.js
```
---
## Constructor

```js
new StudyPlanner()
```

### Properties
```JS
this.details = {
	id: -1,
	status: '',
	course: {},
	intake: {},
	unit_types: [],
	recommended_electives: []
};
// Total credits counter
this.total_combined_credits = 0;
// Elective counter
this.elective_counter = 0;
this.years = [];
this.semester_state = {
	added: [], //Should the Year and the Semester type
	removed: [], //Should be the ID that it wants to be removed
}
this.units_state = {
	added: [], //The semester_id that it will be added to
	edited: [], //Only if both is existing in database, it can be edited
	removed: [], //Only if it existing in database, it can be removed
}
```
---

## Getters & Setters
| Name                 | Returns | Description                                                         |
| -------------------- | ------- | ------------------------------------------------------------------- |
| courseName           | string  | The name of the course.                                             |
| courseCode           | string  | The code of the course.                                             |
| status               | string  | The status of the planner.                                          |
| intakeYear           | number  | The intake year.                                                    |
| majorName            | string  | The name of the major.                                              |
| creditsRequired      | number  | The required credits for the course.                                |
| intakeName           | string  | The intake name.                                                    |
| intakeMonth          | string  | The intake month.                                                   |
| unit_types           | Array   | The array of unit types.                                            |
| recommendedElectives | Array   | The array of recommended electives. (No functionality included yet) |
| totalCredits         | number  | The total combined credits in the planner.                          |
| allYears             | Array   | The years array.                                                    |

---
## Main Methods

### InitDetails



---
## Helper Functions
These are defined outside the class and used for utility logic:
- `FetchMasterPlannerContext(master_study_planner_id)`
- `BuildYearsFromData({...})`
- `CheckMinCP(years, req, targetYear, targetSemIndex, master_mode)`
- `CheckPrerequisite(years, req, targetYear, targetSemIndex, master_mode)`
- `CheckCorequisite(years, req, targetYear, targetSemIndex, master_mode)`
- `CheckAntirequisite(years, req, targetYear, targetSemIndex, master_mode)`
- `DetermineNextIntake(last_intake_month, last_intake_year, semType)`
- `FindLastSemesterFromPreviousYears(startYear, years)`

---
## Example Usage

```js
import StudyPlanner from './StudyPlanner';

const planner = new StudyPlanner();
await planner.Init(master_study_planner_id);
planner.AddNewYear();
planner.AddNewSemester(2, "Long Semester");
planner.SaveToDB();
```

---
## Export
The class is exported as the default export from the module.
```js
export default StudyPlanner;
```