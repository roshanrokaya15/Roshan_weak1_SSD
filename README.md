# 💻 SSD Week 1: Environment Setup & OO Reference Architecture
**Software Systems Development (CRN 12391) · Level 5**  
**The British College (Leeds Beckett University) · Sudan Pudasaini**

---

> [!IMPORTANT]
> ### 📢 Notice for Students: Code is Already Complete!
> **You do NOT need to write missing code or implement methods from scratch.**  
> This repository is a **fully working Object-Oriented reference architecture** designed to verify your development environment (Java 21, Maven, IDE, and GitHub workflow).  
> 
> **Your primary task is to:**
> 1. Clone this repository and open it in your IDE.
> 2. Inspect the reference code to understand real-world OOP patterns (Inheritance, Abstraction, Polymorphism, and Defensive Programming).
> 3. Run the application and JUnit 5 test suite to verify your environment works.
> 4. Fill in your details in [**`SETUP.md`**](SETUP.md).
> 5. Commit and push your changes to GitHub to trigger the automated build.

---

## 🎯 Learning Objectives

By completing this lab walkthrough, you will:
1. **Verify Your Environment:** Confirm that **JDK 21**, Maven, and your IDE (IntelliJ IDEA, Eclipse, or VS Code) compile and run Java projects smoothly.
2. **Review Object-Oriented Core Principles in Java:**
   - **Encapsulation:** Private state variables with validated getters and setters.
   - **Defensive Programming & Invariants:** Throwing `IllegalArgumentException` to block invalid states (e.g., negative radius, impossible triangle sides).
   - **Inheritance & Constructor Chaining:** Utilizing `extends` and forwarding state to `super()`.
   - **Abstraction:** Defining an `abstract class` with abstract contracts (`getArea()`, `getPerimeter()`).
   - **Polymorphism & Dynamic Dispatch:** Storing concrete objects in generic collections (`List<Shape>`) and invoking polymorphic methods at runtime.
3. **Automated Testing:** Run and observe unit tests with JUnit 5.
4. **Course Onboarding:** Complete and submit your course profile and Component 1 team preferences in [**`SETUP.md`**](SETUP.md).

---

## 🧭 Step-by-Step Student Workflow

```mermaid
flowchart LR
    A[1. Clone Repo & Open in IDE] --> B[2. Inspect Architecture & Code]
    B --> C[3. Run Driver & Tests]
    C --> D[4. Fill Out SETUP.md]
    D --> E[5. Commit & Push to GitHub]
```

### Step 1: Clone and Open in Your IDE
1. Open your terminal or Git client and clone your repository:
   ```bash
   git clone <YOUR_REPOSITORY_URL>
   cd ssd-2026-week1-starter
   ```
2. Open the project folder in your preferred IDE:
   - **IntelliJ IDEA (Recommended):** `File` $\rightarrow$ `Open...` $\rightarrow$ Select `pom.xml` $\rightarrow$ `Open as Project`.
   - **VS Code:** Open folder and ensure the *Extension Pack for Java* is active.
   - **Eclipse:** `File` $\rightarrow$ `Import...` $\rightarrow$ `Existing Maven Projects`.
3. Confirm that the project SDK is set to **Java 21**.

---

### Step 2: Code Architecture Tour (What Each Class Does)

Take 10–15 minutes to inspect the files under `src/main/java/shapes/`:

| File | OOP Concept Demonstrated | Key Implementation Detail |
|---|---|---|
| [`Shape.java`](src/main/java/shapes/Shape.java) | **Abstraction & Base Encapsulation** | Declared `abstract`. Holds encapsulated `numberOfSides` with `super(sides)`. Declares abstract contracts: `getArea()` and `getPerimeter()`. |
| [`Square.java`](src/main/java/shapes/Square.java) | **Inheritance & Invariants** | Extends `Shape`. Calls `super(4)`. Rejects non-positive side lengths via `IllegalArgumentException`. |
| [`Circle.java`](src/main/java/shapes/Circle.java) | **Constructor Chaining & Math API** | Extends `Shape`. Calls `super(0)` (no straight sides). Encapsulates `radius` and uses `Math.PI` for area ($\pi r^2$) and circumference ($2\pi r$). |
| [`Triangle.java`](src/main/java/shapes/Triangle.java) | **Complex Domain Invariants** | Extends `Shape`. Calls `super(3)`. Validates the **Triangle Inequality Theorem** ($a + b > c$, $a + c > b$, $b + c > a$) before allowing object instantiation. Computes area via **Heron's Formula**: $\sqrt{s(s-a)(s-b)(s-c)}$. |
| [`Driver.java`](src/main/java/shapes/Driver.java) | **Polymorphism & Dynamic Dispatch** | Creates a `List<Shape>` containing a Square, Circle, and Triangle. Loops over the list to print areas and perimeters using runtime dynamic dispatch. |

---

### Step 3: Run the Application and JUnit 5 Tests

#### A. Run the Driver Program
Run `Driver.java` directly in your IDE (or via terminal):
```bash
# In your IDE: Right-click Driver.java -> Run 'Driver.main()'
```
**Expected Output:**
```text
Shape: Square (sides: 4), Area: 25.00, Perimeter: 20.00
Shape: Circle (sides: 0), Area: 28.27, Perimeter: 18.85
Shape: Triangle (sides: 3), Area: 6.00, Perimeter: 12.00
```

#### B. Run the Automated Test Suite
Open `src/test/java/shapes/ShapeTest.java` and run the tests:
- **In IDE:** Click the green **Run** arrow next to `public class ShapeTest`.
- **In Terminal:**
  ```bash
  mvn test
  ```
**Expected Result:**
All tests pass with green checkmarks:
- ✅ `testSquareAreaAndPerimeter()`
- ✅ `testSquareThrowsOnZeroOrNegative()`
- ✅ `testCircleAreaAndPerimeter()`
- ✅ `testCircleThrowsOnZeroOrNegative()`
- ✅ `testTriangleAreaAndPerimeter()`
- ✅ `testTriangleThrowsOnInvalidSides()`
- ✅ `testPolymorphismList()`

---

### Step 4: Fill Out Your Deliverable (`SETUP.md`)

Open [**`SETUP.md`**](SETUP.md) and fill in your details:
1. **Student Information:** Your full name, Leeds Beckett ID, college email, and GitHub handle.
2. **Environment Verification:** Output of `java -version` and your chosen IDE.
3. **Component 1 Team Preferences:** Your preferred team role and candidate project topics from the approved syllabus list.

---

### Step 5: Commit and Push to GitHub

Once you have filled out [**`SETUP.md`**](SETUP.md), commit and push your work:

```bash
git add SETUP.md
git commit -m "Complete Week 1 setup verification and student profile"
git push origin main
```

> [!TIP]
> After pushing, check your repository on GitHub. Look for the **Actions** tab to confirm that the automated CI workflow executes and displays a green checkmark!

---

## 🌟 Optional Self-Study Challenge (For Extra Practice)

If you have completed the verification steps and want hands-on coding practice before Week 2:

1. **Create a `Rectangle.java` class** in `src/main/java/shapes/`:
   - Extend `Shape` and pass `4` to `super(4)`.
   - Add private fields `width` and `height`.
   - Validate that `width > 0` and `height > 0`.
   - Override `getArea()` and `getPerimeter()`.
2. **Add unit tests** in `src/test/java/shapes/ShapeTest.java` to verify:
   - Correct calculation of area and perimeter for rectangle dimensions.
   - Proper exception thrown when initialized with invalid values (zero or negative).
3. Add a `Rectangle` instance to the list in `Driver.java` and verify output.

---

## ❓ Frequently Asked Questions & Troubleshooting

<details>
<summary><b>Q1: My IDE says "Cannot resolve symbol 'Shape'" or red squiggly lines appear.</b></summary>
Your IDE has not recognized the project as a Maven project yet.
- In IntelliJ: Right-click <code>pom.xml</code> $\rightarrow$ <b>Maven</b> $\rightarrow$ <b>Reload Project</b>.
- In VS Code: Run <code>Java: Clean Java Language Server Workspace</code> from the Command Palette (<code>Ctrl+Shift+P</code> / <code>Cmd+Shift+P</code>).
</details>

<details>
<summary><b>Q2: <code>mvn: command not found</code> in my terminal.</b></summary>
If Maven is not installed globally on your machine, you can run all tests and applications directly using your IDE's built-in test runner (e.g. IntelliJ's green play button on <code>ShapeTest</code>).
</details>

<details>
<summary><b>Q3: Where can I review the theory behind vtables, dynamic dispatch, and Heron's formula?</b></summary>
See the comprehensive lecture guide in <a href="CLASS_2_NOTES_AND_LAB_GUIDE.md"><code>CLASS_2_NOTES_AND_LAB_GUIDE.md</code></a>.
</details>

---

*Module: Software Systems Development (CRN 12391) · The British College, Kathmandu*  
*Lecturer: Sudan Pudasaini · Awarded by Leeds Beckett University*
