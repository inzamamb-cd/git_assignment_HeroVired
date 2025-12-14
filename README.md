# 🚀 Git Assignment: Calculator Plus App

This repository, `git_assignment_HeroVired`, is used to demonstrate key Git workflow steps including branching, feature development, bug fixing, merging, and releasing versions of a simple Python calculator application.

## 📋 Prerequisites

Before starting, ensure you have:
* Git installed on your system.
* A GitHub/GitLab/Bitbucket account.

## 🛠️ Assignment Steps

Follow the steps below to complete the assignment.

### a. Create the Repository

1.  Create a new repository named **`git_assignment_HeroVired`** on your Git hosting service (e.g., GitHub).
2.  Clone the repository to your local machine:

    ```bash
    git clone [https://github.com/YourUsername/git_assignment_HeroVired.git](https://github.com/YourUsername/git_assignment_HeroVired.git)
    cd git_assignment_HeroVired
    ```

### b. Create the Initial Code on the 'dev' Branch

1.  Create and switch to a new branch named `dev`:

    ```bash
    git checkout -b dev
    ```

2.  Create a file named **`calculator.py`** and add the following initial code:

    ```python
    import math

    class Calculator:
        def add(self, a, b):
            return a + b

        def subtract(self, a, b):
            return a - b

        def multiply(self, a, b):
            return a * b

        def divide(self, a, b):
            return a / b

        # TODO: Implement the following function to calculate the square root of a number.
        # def square_root(self, x):
        #     return math.sqrt(x)

    if __name__ == "__main__":
        calculator = Calculator()
        num1 = 16
        num2 = 4
        print(f"{num1} + {num2} = {calculator.add(num1, num2)}")
        print(f"{num1} - {num2} = {calculator.subtract(num1, num2)}")
        print(f"{num1} * {num2} = {calculator.multiply(num1, num2)}")
        print(f"{num1} / {num2} = {calculator.divide(num1, num2)}")
        # TODO: Uncomment and test the square root feature.
        # num3 = 25
        # print(f"The square root of {num3} = {calculator.square_root(num3)}")
    ```

3.  Commit the changes and push the `dev` branch to the remote:

    ```bash
    git add calculator.py
    git commit -m "Initial calculator implementation on dev branch"
    git push -u origin dev
    ```

### c. Merge to main and Release Version 1

1.  Switch back to the `main` branch:

    ```bash
    git checkout main
    ```

2.  Merge the `dev` branch into `main`:

    ```bash
    git merge dev
    ```

3.  Push the changes to the remote `main` branch:

    ```bash
    git push origin main
    ```

4.  **Create Release v1.0.0:** On your Git hosting platform (e.g., GitHub Releases), create a new release with the tag **`v1.0.0`** and the title "Version 1 - Initial Calculator Plus App".

### d. Add Classmate as Collaborator

1.  Go to the **"Settings"** page of your repository on your Git hosting service.
2.  Navigate to **"Collaborators"** or **"Manage access"**.
3.  Add the GitHub username of one of your classmates as a collaborator.

### e. & f. Implement 'sqrt' Feature

1.  Create and switch to a new feature branch named `feature/sqrt` based on the `dev` branch:

    ```bash
    git checkout dev
    git checkout -b feature/sqrt
    ```

2.  Open **`calculator.py`** and **uncomment and complete** the `square_root` function and the test code in `if __name__ == "__main__":`.

    **Updated `calculator.py` (Snippet):**

    ```python
    # ... (rest of the code)

        def divide(self, a, b):
            return a / b

        # TODO: Implement the following function to calculate the square root of a number.
        def square_root(self, x):
             return math.sqrt(x) # Implementation added

    if __name__ == "__main__":
        # ... (rest of the test code)
        print(f"{num1} / {num2} = {calculator.divide(num1, num2)}")
        # TODO: Uncomment and test the square root feature.
        num3 = 25 # Uncommented
        print(f"The square root of {num3} = {calculator.square_root(num3)}") # Uncommented and tested
    ```

3.  Commit the feature implementation:

    ```bash
    git add calculator.py
    git commit -m "feat: Add square root function"
    git push -u origin feature/sqrt
    ```

### g. Critical Bug Fix (Hotfix)

While working on `feature/sqrt`, a critical bug is reported in the `divide` function in the `dev` branch.

1.  **Stash the current changes** in `feature/sqrt` so you can switch branches cleanly:

    ```bash
    git stash push -m "WIP on sqrt feature"
    ```

2.  Switch to the `dev` branch:

    ```bash
    git checkout dev
    ```

3.  Open **`calculator.py`** and apply the bug fix to the `divide` function:

    **Updated `divide` function (Snippet):**

    ```python
        def divide(self, a, b):
            if b == 0:
                raise ValueError("Cannot divide by zero.")
            return a / b
    ```

4.  Commit the fix and push to the remote `dev` branch:

    ```bash
    git add calculator.py
    git commit -m "fix: Prevent division by zero error"
    git push origin dev
    ```

5.  Switch back to the feature branch:

    ```bash
    git checkout feature/sqrt
    ```

6.  **Rebase** the feature branch onto the updated `dev` branch to include the fix and keep the history linear:

    ```bash
    git rebase dev
    ```
    * *Note: If there were conflicts, you would resolve them here.*

7.  Apply the stashed changes back onto the `feature/sqrt` branch:

    ```bash
    git stash pop
    ```
    * *This should merge cleanly as the fix was in a different part of the file.*

8.  Push the rebased branch (might require `--force-with-lease` if you rebased remote commits, but for a new feature branch, a normal push often suffices after a rebase):

    ```bash
    git push origin feature/sqrt --force-with-lease
    ```

### h. & i. Create Pull Request and Review

1.  Go to your Git hosting service and **create a Pull Request (PR)** from `feature/sqrt` into the `dev` branch.
2.  **Request a code review** from the collaborator you added in step (d).
3.  Based on the review, make any necessary improvements, commit, and push them to the `feature/sqrt` branch.

### j. Merge 'feature/sqrt' into 'dev'

1.  Once the code reviewer approves the PR, **merge the `feature/sqrt` branch into `dev`** (preferably using a **Squash and Merge** or **Rebase and Merge** option if available, to keep the `dev` history clean).
2.  Alternatively, you can merge locally and push:

    ```bash
    git checkout dev
    git merge feature/sqrt --no-ff # Use --no-ff to always create a merge commit
    git push origin dev
    ```

### k. Final Testing, Merge to main, and Release Version 2

1.  **Testing in `dev` branch:** Locally run the `calculator.py` on the `dev` branch to ensure all features (including `sqrt`) and the bug fix (division by zero) work as expected.

    ```bash
    python calculator.py
    # Test division by zero
    # print(calculator.divide(16, 0)) # Should raise an error
    ```

2.  Merge the stable `dev` branch into `main`:

    ```bash
    git checkout main
    git merge dev
    git push origin main
    ```

3.  **Create Release v2.0.0:** On your Git hosting platform, create a new release with the tag **`v2.0.0`** and the title "Version 2 - Square Root Feature and Bug Fix".