## Expense Tracker Application (Skeleton)

This repository contains a small Python backend application that demonstrates:

- Tracking daily expenses
- Categorising expenses (Food, Transport, Entertainment, etc.)
- Setting monthly budgets per category
- Basic alerts when a category budget is exceeded or close to the limit
- Simple monthly reports (total spending and spending vs budget per category)

The implementation uses **Flask**, **Flask-SQLAlchemy**, and **SQLite** to keep
the setup lightweight for local runs and Docker.

> Important: This README is intentionally high-level. You should adapt the
> structure, wording, and code to match your own style and the expectations of
> your assignment instructions.

### 1. Tech stack

- **Python** 3.12 (should also work with recent 3.x versions)
- **Flask** for HTTP routing
- **Flask-SQLAlchemy / SQLAlchemy** as ORM
- **SQLite** as embedded database
- **Docker** for containerised build and run

### 2. Local setup (without Docker)

1. Create and activate a virtual environment:

   ```bash
   python -m venv .venv
   .venv\Scripts\activate  # on Windows PowerShell
   # source .venv/bin/activate  # on Linux / macOS
   ```

2. Install Python dependencies:

   ```bash
   pip install -r requirements.txt
   ```

3. Run the application:

   ```bash
   set FLASK_ENV=development  # on Windows (optional)
   python app.py
   ```

4. Open a browser and navigate to:

   - `http://localhost:5000/`

### 3. Docker build and run

1. Build the image:

   ```bash
   docker build -t expense-tracker .
   ```

2. Run a container:

   ```bash
   docker run --rm -p 5000:5000 expense-tracker
   ```

3. Open the same URL in a browser:

   - `http://localhost:5000/`

The SQLite database file `expenses.db` will be created inside the container
filesystem by default. To persist data between runs, you could mount a volume
and point `DATABASE_URL` to a host path (not strictly necessary for evaluation).

### 4. Basic usage and test flow (examples)

Below is an example sequence you can use as a reference when designing your own
test cases for the assignment.

- **Create user**
  - Go to the landing page and create a user with a name and optional email.
  - After creation, return to the user list and open that user's dashboard.

- **Define categories**
  - From the dashboard, open the categories page.
  - Add several categories such as "Food", "Transport", "Entertainment".

- **Set budgets**
  - Navigate to the budgets page.
  - Choose a month (for example, the current month).
  - For each category, set a budget amount and save.

- **Log expenses**
  - Open the "Log an expense" screen.
  - Create a few expenses on different dates, with different categories and
    positive amounts.

- **View expenses and report**
  - Open the "View recent expenses" screen to check the raw entries.
  - Open the monthly report screen, pick a month and verify:
    - Total spending for the month.
    - Per-category budget, actual spend, and remaining amount.

### 5. Example edge cases (for your own tests)

When you document your own test steps, consider the following scenarios:

- **Budget exceeded**
  - Set a small budget for a category (for example 100).
  - Add expenses whose sum crosses 100 in that month.
  - Confirm that the UI indicates that the budget is exceeded.

- **10% remaining alert**
  - Set a budget of 100 for a category.
  - Add expenses so that total is in the 90–100 range.
  - Confirm that the UI shows that only a small fraction (10% or less)
    is available.

- **No budget defined**
  - Add expenses in a category for a month with no explicit budget.
  - Decide how your implementation should behave (for example:
    treat as uncapped or treat as zero budget) and document it.

- **Invalid input**
  - Try to submit an expense with negative or zero amount.
  - Try to submit an invalid date.
  - Ensure that validation errors are shown instead of saving the data.

### 6. ORM / SQL note

The application uses SQLAlchemy's ORM for defining models and performing common
queries (see `models.py` and query usage in `app.py`). You can extend this with
additional raw SQL queries if your assignment explicitly requires a handwritten
SQL example.

### 7. Next steps for your assignment

- Review the code and structure it according to your own preferences.
- Rename functions, templates, and variables as needed.
- Rewrite the README sections in your own words.
- Add or modify test cases so that they fully reflect the behaviour you want
  to demonstrate to the evaluators.


