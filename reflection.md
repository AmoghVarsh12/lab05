1.Which issues were the easiest to fix, and which were the hardest? Why?

Answer :
EASIEST
**Style/Formatting Issues (Flake8 E302, E303, E305)**
Adding blank lines between functions
Fix: Just add or remove blank lines as needed

HARDEST
**Security Issue - eval() Usage (Bandit B307, Pylint W0123)**
`eval()` can execute arbitrary code and is a major security risk
Had to understand the intent and replace with safe alternative
Fix: Removed `eval()` completely and used direct print statement



2. Did the static analysis tools report any false positives? If so, describe one example.

Answer:

**Yes, there was at least one arguable false positive:**

**Pylint W0603: Using the global statement (global-statement)**
Location: `load_data()` function
The warning flags the use of `global stock_data`
Pylint considers global variables a code smell and warns against them

**Why this could be considered a false positive:**

 **Context matters**: In this small inventory system, using a global variable for `stock_data` is a reasonable design choice
 **Intentional design**: The global variable serves as a simple in-memory database for the application
 **Alternative would be overkill**: Pylint would prefer passing the dictionary around as parameters or using a class, but for this simple script, that adds unnecessary complexity
 **Legitimate use case**: The `load_data()` function needs to replace the entire global dictionary, which is exactly what the global statement is designed for


 3. How would you integrate static analysis tools into your actual software development workflow? Consider continuous integration (CI) or local development practices.

Answer:
Yes I would consider using these tools, as :

Catches issues before they enter version control
Forces developers to fix issues immediately
Reduces code review burden
Configure VS Code with real-time linting:
Immediate feedback while coding
Visual indicators (squiggly lines) for issues
Learn best practices through real-time guidance
Automate checks on every pull request:



4.What tangible improvements did you observe in the code quality, readability, or potential
robustness after applying the fixes?

Answer:
**Security:** Eliminated critical vulnerabilities (eval injection, bare exceptions) that could crash the program or execute malicious code.
**Reliability:** Fixed undefined function bug (removeItem) and dangerous default argument ([]) that caused data corruption across function calls.
**Readability:** Added comprehensive docstrings and consistent snake_case naming, making the code self-documenting and immediately understandable.
**Maintainability:** Proper error handling with specific exceptions and informative messages enables faster debugging and reduces production issues.
**Professionalism:** Code went from Pylint score 3.06/10 to 10/10, following Python best practices and PEP 8 standards for production-ready quality.

