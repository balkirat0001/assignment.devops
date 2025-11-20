# Git Merge Conflict Assignment - Documentation

## Project Overview
**Project Name:** Simple Calculator  
**Repository URL:** https://github.com/balkirat0001/assignment.devops.git  
**Date:** November 20, 2025

## Project Description
This project is a simple web-based calculator built using HTML5, CSS3, and JavaScript. The calculator supports basic arithmetic operations and features a modern, responsive design with gradient styling.

---

## Git Workflow Steps

### Step 1: Project Initialization
```powershell
# Initialize Git repository
git init

# Configure Git user
git config user.name "balkirat0001"
git config user.email "balkirat0001@users.noreply.github.com"
```

### Step 2: Initial Commit
Created the following files:
- `index.html` - Main calculator interface
- `styles.css` - Styling with gradient design
- `script.js` - Calculator functionality
- `README.md` - Project documentation

```powershell
# Add all files to staging area
git add .

# Create initial commit
git commit -m "Initial commit: Added simple calculator with HTML, CSS, and JavaScript"

# Rename branch to main
git branch -M main
```

### Step 3: Connect to GitHub Remote
```powershell
# Add remote repository
git remote add origin https://github.com/balkirat0001/assignment.devops.git
```

### Step 4: Create First Feature Branch
```powershell
# Create and switch to feature-scientific branch
git checkout -b feature-scientific
```

**Changes Made:** Added scientific calculator features to README.md
- Modified the Features section to include: "Scientific functions (square root, power, trigonometry)"

```powershell
# Stage and commit changes
git add README.md
git commit -m "Added scientific calculator features to README"
```

### Step 5: Create Second Feature Branch (Conflicting)
```powershell
# Switch back to main
git checkout main

# Create and switch to feature-themes branch
git checkout -b feature-themes
```

**Changes Made:** Added theme customization to README.md (same location)
- Modified the Features section to include: "Multiple color themes (dark mode, light mode)"

```powershell
# Stage and commit changes
git add README.md
git commit -m "Added features to README"
```

### Step 6: Merge First Branch (No Conflict)
```powershell
# Switch to main branch
git checkout main

# Merge feature-scientific branch
git merge feature-scientific
```

**Result:** Fast-forward merge completed successfully. Main branch now includes scientific features.

### Step 7: Merge Second Branch (Conflict Occurs)
```powershell
# Attempt to merge feature-themes branch
git merge feature-themes
```

**Result:** Merge conflict detected!
```
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
```

---

## Understanding the Merge Conflict

### What Caused the Conflict?
The merge conflict occurred because:
1. Both `feature-scientific` and `feature-themes` branches modified the **same section** of the `README.md` file
2. Specifically, both branches added a new line in the Features list after "Basic arithmetic operations"
3. When `feature-scientific` was merged first, main branch contained the scientific features line
4. When attempting to merge `feature-themes`, Git couldn't automatically decide which change to keep

### Conflict Visualization

**Before Merge:**
- Main branch (after first merge): Has scientific functions line
- Feature-themes branch: Has color themes line (same position)

**Conflict Markers in README.md:**
```markdown
## Features
- Basic arithmetic operations (addition, subtraction, multiplication, division)
<<<<<<< HEAD
- Scientific functions (square root, power, trigonometry)
=======
- Multiple color themes (dark mode, light mode)
>>>>>>> feature-themes
- Clear and delete functions
```

**Explanation of Markers:**
- `<<<<<<< HEAD` - Marks the beginning of the current branch (main) changes
- `=======` - Separates the two conflicting versions
- `>>>>>>> feature-themes` - Marks the end of the incoming branch changes

---

## Conflict Resolution Process

### Step 1: Check Git Status
```powershell
git status
```

**Output:**
```
On branch main
You have unmerged paths.
  (fix conflicts and run "git commit")
  
Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   README.md
```

### Step 2: View the Diff
```powershell
git diff
```

This command showed the conflicting sections with conflict markers.

### Step 3: Manual Resolution
Opened `README.md` and manually edited the file to keep BOTH features:

**Resolved Version:**
```markdown
## Features
- Basic arithmetic operations (addition, subtraction, multiplication, division)
- Scientific functions (square root, power, trigonometry)
- Multiple color themes (dark mode, light mode)
- Clear and delete functions
- Keyboard support
- Modern gradient design
- Responsive layout
```

**Resolution Strategy:** Combined both features since they are complementary and not mutually exclusive.

### Step 4: Stage Resolved File
```powershell
git add README.md
```

### Step 5: Verify Resolution
```powershell
git status
```

**Output:**
```
On branch main
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

Changes to be committed:
        modified:   README.md
```

### Step 6: Complete the Merge
```powershell
git commit -m "Resolved merge conflict: Combined scientific and theme features"
```

---

## Final Git History

```powershell
git log --oneline --graph --all
```

**Result:**
```
*   116a78f (HEAD -> main) Resolved merge conflict: Combined scientific and theme features
|\
| * 19a5768 (feature-themes) Added features to README
* | a6fbcf1 (feature-scientific) Added scientific calculator features to README
|/
* e514e4c Initial commit: Added simple calculator with HTML, CSS, and JavaScript
```

This graph shows:
- Main branch started with initial commit
- Two branches diverged from main
- Both branches were merged back, creating a merge commit
- The asterisk (*) shows the current HEAD position

---

## Push to GitHub

```powershell
# Push main branch
git push -u origin main

# Push feature branches
git push origin feature-scientific feature-themes
```

All branches successfully pushed to: https://github.com/balkirat0001/assignment.devops.git

---

## Key Git Commands Used

| Command | Purpose |
|---------|---------|
| `git init` | Initialize repository |
| `git add` | Stage files for commit |
| `git commit` | Create commit with changes |
| `git branch -M main` | Rename branch to main |
| `git remote add origin <url>` | Connect to remote repository |
| `git checkout -b <branch>` | Create and switch to new branch |
| `git checkout <branch>` | Switch to existing branch |
| `git merge <branch>` | Merge branch into current branch |
| `git status` | Check repository status |
| `git diff` | View changes and conflicts |
| `git log --graph --oneline --all` | View commit history |
| `git push` | Upload changes to remote |

---

## Reflective Note

### What I Learned About Merge Conflicts

**Understanding the Conflict:**
Merge conflicts occur when Git cannot automatically reconcile differences between two branches. In this project, the conflict happened because both feature branches modified the exact same lines in the README.md file. Git requires human intervention to decide which changes to keep because it cannot make assumptions about the developer's intent.

**Resolution Process:**
Resolving the conflict taught me the importance of:
1. **Careful Code Review** - Reading both versions to understand what each branch was trying to accomplish
2. **Decision Making** - Choosing whether to keep one version, the other, or combine both
3. **Testing** - Ensuring the merged result makes logical sense and maintains file integrity
4. **Communication** - Writing clear commit messages that explain the resolution

**Distributed Version Control Benefits:**
This exercise demonstrated key advantages of Git:
- **Parallel Development** - Multiple developers can work on different features simultaneously without blocking each other
- **Branch Isolation** - Each feature can be developed independently without affecting the main codebase
- **Safe Experimentation** - If a merge conflict is too complex, you can abort the merge and try a different approach
- **Complete History** - Git preserves the entire development history, making it easy to understand how the codebase evolved

**Best Practices Discovered:**
1. **Frequent Pulls/Updates** - Regularly updating from main branch reduces the likelihood of conflicts
2. **Small, Focused Commits** - Smaller changes are easier to merge and conflicts are easier to resolve
3. **Clear Branch Naming** - Descriptive branch names help understand the purpose of changes
4. **Communication** - In team settings, coordinating who modifies which files can prevent conflicts

**Practical Applications:**
In real-world development:
- Conflicts are common when multiple developers work on the same codebase
- Version control systems like Git are essential for managing complex projects
- Understanding how to resolve conflicts efficiently is a critical skill
- Merge conflicts often highlight areas where better code organization could help

This assignment provided hands-on experience with Git's conflict resolution workflow, demonstrating why version control is fundamental to modern software development. The ability to manage parallel development streams and safely integrate changes is what makes distributed version control systems invaluable for both individual and team projects.

---

## Project Files

### index.html
Complete HTML structure for the calculator with:
- Display screen
- Number buttons (0-9)
- Operation buttons (+, -, *, /)
- Clear and Delete functionality
- Equals button for calculation

### styles.css
Modern styling featuring:
- Purple gradient background
- Dark themed calculator design
- Hover effects on buttons
- Responsive layout

### script.js
JavaScript functionality including:
- Arithmetic operations
- Display management
- Error handling
- Keyboard support

### README.md
Project documentation with:
- Project description
- Features list (including resolved merge conflict)
- Technologies used
- Setup instructions

---

## Conclusion

This project successfully demonstrated:
✅ Git initialization and repository setup  
✅ Branching and parallel development  
✅ Committing and version tracking  
✅ Intentional merge conflict creation  
✅ Conflict identification and resolution  
✅ Remote repository integration  
✅ Complete Git workflow understanding  

The calculator application serves as a practical example of managing version control in a real project, and the intentional merge conflict provided valuable hands-on experience with conflict resolution—a skill essential for collaborative software development.
