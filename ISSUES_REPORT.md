# Template Audit & Friction Points — Student Semester Planner & GPA Calculator

## 1. Logo Hosting Issue (Notion API)
- **Problem:** The Notion API `icon` property does not support direct local file uploads.
- **Resolution:** Distribute `moorish_dev_logo.png` to `assets/`. User must manually set it as the page icon in the Notion UI.

## 2. Multi-Database Relation Setup
- **Problem:** The template requires a Relation between a `Courses` database and an `Assignments` database. While the Notion API supports creating relations, the specific "backlink" behavior and rollup formulas may need manual configuration in the UI.
- **Resolution:** The automated build will create both databases and add the Relation property. The user must verify the Rollup configurations (e.g., count of assignments per course, average grade) are correctly set in the Notion UI as documented in `docs/Database_Schema.md`.

## 3. GPA Formula Complexity
- **Problem:** The GPA calculation formula is a nested `if()` chain. The Notion API may have difficulties creating complex Formula properties via the `properties` endpoint without triggering validation errors.
- **Resolution:** The `GPA` property will be staged as a `Number` type during automated build. User must manually convert it to a `Formula` type and paste the snippet from `docs/Database_Schema.md`.

## 4. Button Block API Limitation
- **Problem:** Notion's native Button blocks cannot be created via the public Notion API.
- **Resolution:** User must manually create Button blocks (`📚 New Course`, `📝 New Assignment`) inside the Notion UI following `setup_guide/Setup_Guide.md`.

## 5. Calendar View for Assignments
- **Problem:** A Calendar view (by Due Date) is critical for student usability, but view configurations must be set manually in the Notion UI.
- **Resolution:** After automated setup, user must add a Calendar view to the Assignments Linked View on the dashboard.
