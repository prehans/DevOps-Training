Devops Notes

The challenges with the SDLC (Software Development Lifecycle) and toolchain complexity are common as organizations grow and their development processes become more sophisticated. Let's break down each of these issues in detail:

### 1. **Redundant and Incompatible Tools**

**Problem:**
As organizations adopt different tools for various stages of the SDLC (e.g., planning, development, testing, deployment), they often end up with multiple tools that perform similar functions or don’t integrate well with each other. This redundancy can lead to inefficiencies and confusion.

**Implications:**

- **Duplication of Effort:** Teams may enter or manage the same information in multiple systems.
- **Increased Costs:** Licensing and maintenance of multiple tools can be expensive.
- **Tool Fatigue:** Users may become overwhelmed by the number of tools they need to use.

### 2. **Data and Process Silos**

**Problem:**
Disparate tools often result in data being stored in separate locations or formats, leading to silos where information isn’t easily accessible across the organization.

**Implications:**

- **Fragmented Insights:** Teams may lack a unified view of project status, making it difficult to understand overall progress and performance.
- **Inefficient Workflows:** Information needs to be manually transferred between tools or teams, which can be error-prone and time-consuming.
- **Delayed Decision-Making:** Lack of integrated data can slow down decision-making processes due to incomplete or inconsistent information.

### 3. **No Alignment Among Teams**

**Problem:**
When tools and processes aren’t integrated, different teams may follow different workflows and use different tools for similar tasks.

**Implications:**

- **Miscommunication:** Teams may have different understandings of project requirements or status.
- **Conflicting Priorities:** Without a shared view of project goals and progress, teams might work towards conflicting objectives.
- **Reduced Collaboration:** Disparate tools can hinder effective communication and collaboration among team members.

### 4. **No Consistent Application Security or Compliance**

**Problem:**
Without a unified approach, security and compliance practices may be applied inconsistently across different stages of the SDLC or between tools.

**Implications:**

- **Security Risks:** Inconsistent application of security practices can leave vulnerabilities exposed.
- **Compliance Issues:** Ensuring compliance with regulations and standards becomes more difficult if practices aren’t standardized.
- **Increased Risk of Breaches:** Lack of integration can lead to gaps in security monitoring and response.

### 5. **No Consistent Traceability**

**Problem:**
Traceability refers to the ability to track the history and changes of code, requirements, and issues throughout the SDLC.

**Implications:**

- **Difficulty in Audits:** It’s harder to audit changes and understand their impact when traceability is inconsistent.
- **Challenge in Troubleshooting:** Identifying the root cause of issues can be more difficult without clear traceability.
- **Reduced Accountability:** Lack of clear history can lead to unclear responsibility for decisions and changes.

### 6. **A High Degree of Context Switching**

**Problem:**
Context switching occurs when individuals or teams have to frequently move between different tools or systems to complete their work.

**Implications:**

- **Decreased Productivity:** Constantly switching between tools can disrupt focus and reduce overall productivity.
- **Increased Learning Curve:** Users need to become proficient in multiple tools, which can be time-consuming and mentally taxing.
- **Inconsistent Information:** Context switching can lead to inconsistencies and errors as users may not have all the information they need at their fingertips.

### Solutions and Best Practices

To address these challenges, organizations can consider the following approaches:

- **Adopt Integrated Platforms:** Use platforms that offer end-to-end solutions for managing the SDLC, such as GitLab, which integrates various functions into a single interface.
- **Implement Standardization:** Standardize processes and tools across teams to ensure consistency and reduce redundancy.
- **Improve Integration:** Ensure that tools used across the SDLC can integrate seamlessly with each other to facilitate smooth data flow and collaboration.
- **Automate Processes:** Implement automation where possible to reduce manual data transfer and improve efficiency.
- **Enhance Communication:** Foster better communication and collaboration among teams to align goals and practices.

By addressing these issues proactively, organizations can streamline their SDLC, improve efficiency, and enhance overall project success.

# Overview

![alt text](Images/image.png)

<<<<<<< HEAD

> > > > > > > # e78cf7e0f2f499ba455057d09374e76b03887f3e
> > > > > > >
> > > > > > > 00c57ed18c7e1a7eba518dce1a4b330208eb2b16

# Types of Version Control System

Version control systems (VCS) can be categorized into several types based on their architecture and functionality:

### 1. **Local Version Control Systems**

**Description:** These systems manage versions of files on a local machine. They are useful for tracking changes and managing versions within a single user’s environment.

**Examples:**

- **RCS (Revision Control System):** Tracks changes to files and directories.
- **SCCS (Source Code Control System):** An early system for managing changes to source code.

### 2. **Centralized Version Control Systems (CVCS)**

**Description:** Centralized version control systems store all version history in a central server. Users commit their changes to this central repository and update their local copies from it.

**Examples:**

- **Subversion (SVN):** A widely used CVCS that tracks changes and handles versioning of files and directories.
- **CVS (Concurrent Versions System):** An older system that was popular before more modern VCS solutions emerged.
- **TFS (Team Foundation Server):** Provides version control along with project management and collaboration features.

### 3. **Distributed Version Control Systems (DVCS)**

**Description:** Distributed version control systems allow each user to have a full copy of the repository, including its history. Changes are shared among repositories, and users can work offline.

**Examples:**

- **Git:** A highly popular DVCS known for its branching and merging capabilities, as well as its performance.
- **Mercurial:** Another DVCS similar to Git, known for its simplicity and performance.
- **Bazaar:** A DVCS that provides support for different workflows and integrates well with various development environments.

### 4. **Hybrid Version Control Systems**

**Description:** Hybrid systems combine aspects of both centralized and distributed version control. They allow for both centralized and distributed workflows within the same system.

**Examples:**

- **Perforce Helix Core:** A version control system that can be used in a centralized manner but also supports distributed workflows.
- **BitKeeper:** Originally a commercial DVCS with both centralized and distributed features.

### Summary

- **Local VCS**: Tracks changes on a single machine.
- **Centralized VCS**: Uses a central repository for version control.
- **Distributed VCS**: Each user has a full repository copy and can work offline.
- **Hybrid VCS**: Combines features of both centralized and distributed systems.

Each type of version control system offers different advantages and is suited to different use cases depending on factors such as team size, project complexity, and workflow preferences.

### **Understanding Environment Branches in GitLab**

**1. **Default Branch:\*\*

When you create a new GitLab project, it automatically includes a default branch (often named `master` or `main`). This default branch is where the stable, production-ready code usually resides.

**2. **Environment Branches:\*\*

As projects evolve, teams create additional branches to manage different environments and stages of development. Common types of environment branches include:

- **`production` Branch:** Represents the code that is live in the production environment. It is the stable branch that end-users interact with.
- **`staging` or `pre-production` Branch:** Represents code that is almost ready for production but needs to be tested in an environment that mimics production as closely as possible. This environment is used for final testing and validation.

- **`development` Branch:** Often used for ongoing development and integrating features before they are ready for staging or production.

- **`feature` Branches:** Created for developing specific features or fixes. These branches are eventually merged into the `staging` or `production` branches.

**3. **Workflow with Environment Branches:\*\*

In a typical GitLab workflow involving environment branches:

- **Development:** Developers work on features or fixes in feature branches. These branches are created from the `development` or `staging` branch and contain specific changes.

- **Testing:** Once features are complete, they are merged into the `staging` branch. This branch is deployed to a staging environment where the changes are tested in conditions similar to production.

- **Release:** After successful testing, the `staging` branch is merged into the `production` branch. This ensures that the changes are deployed to the live environment.

- **Cherry-Picking:** If a hotfix (urgent fix) is needed, you can create a feature branch for the fix. This branch is merged into the `master` (or `production`) branch using a merge request. If the hotfix needs to be applied to other branches (like `staging`), you can create additional merge requests from the feature branch to those downstream branches. This ensures that the fix is propagated through all necessary environments.

**4. **Commit Flow:\*\*

In this workflow, commits flow downstream:

- Changes are first integrated into `feature` branches.
- Once validated, they move into the `staging` branch for more thorough testing.
- Finally, changes are merged into the `production` branch.

This ensures that each stage of development is tested progressively, and potential issues are caught early before reaching the production environment.

**5. **Cherry-Picking and Merge Requests:\*\*

If a hotfix is applied, it’s developed on a feature branch and merged into the `master` or `production` branch. If additional testing is required or if the fix needs to be applied to `staging`, you can create merge requests from the feature branch to these downstream branches.

**6. **Branch Deletion:\*\*

After a feature branch is merged, it’s typically deleted to keep the repository clean. However, if the branch is used for important hotfixes or ongoing work, it might be kept until the associated changes are fully integrated and tested across all relevant branches.

### **Summary**

- **Default Branch**: Stable branch (e.g., `master` or `main`).
- **Environment Branches**: Represent different stages like `production`, `staging`, and `development`.
- **Workflow**: Commits flow from feature branches → staging → production.
- **Cherry-Picking**: For urgent fixes, create feature branches and merge into necessary branches, ensuring changes propagate correctly.
- **Branch Management**: Delete branches after merging to keep the repository organized, but retain important branches as needed.

This structured approach helps manage and deploy code efficiently, ensuring stability and quality through multiple stages of development and testing.

### **Release Branches Overview**

**1. **Purpose of Release Branches:\*\*

Release branches are used to prepare and finalize software for a specific version or release. They allow you to stabilize and make last-minute adjustments before the software is released to users. Release branches typically follow a versioning scheme like `2.3-stable` or `2.4-stable`.

### **Workflow with Release Branches**

**1. **Creating Release Branches:\*\*

- **Creation:** When you’re ready to start preparing for a release, you create a release branch from the main development branch (often `master` or `main`). For example:

  ```bash
  git checkout -b release/2.3-stable
  ```

- **Purpose:** This branch is used to finalize the release. You can perform tasks like bug fixes, testing, and preparing documentation without affecting ongoing development in other branches.

**2. **Merging Changes:\*\*

- **Upstream First Policy:**

  - **Primary Approach:** To maintain consistency, you should follow an "upstream first" policy. This means that all changes, including bug fixes and new features, should first be merged into the main branch (e.g., `master` or `main`).
  - **Cherry-Picking:** After merging changes into the main branch, you can cherry-pick relevant commits into the release branch to ensure that bug fixes and important updates are also included in the release.
  - **Example:**
    ```bash
    git checkout master
    git merge <feature-branch>
    git checkout release/2.3-stable
    git cherry-pick <commit-id>
    ```

- **Tagging:** Once a release branch is finalized and the release is made, a new tag should be created to mark this specific version. Tags help in identifying and referencing specific versions of your software.
  ```bash
  git tag -a v2.3.0 -m "Release version 2.3.0"
  git push origin v2.3.0
  ```

**3. **Stable Branch:\*\*

- **Purpose:** Some projects maintain a `stable` branch that points to the latest released version. This branch provides a reference to the current stable state of the software, even if new release branches are created for future versions.
- **Usage:** The `stable` branch is often updated to reflect the latest stable release. It serves as a reference point and may be used for hotfixes or patches applied to released versions.

**4. **Production Branch:\*\*

- **Common Practice:** In many workflows, a separate `production` branch may not be necessary if the release branches and the `stable` branch effectively cover the needs for production deployment.
- **Alternative:** Instead of a dedicated production branch, the latest release branch or the `stable` branch may serve as the source of truth for what's currently in production.

### **Summary of Key Points**

- **Release Branches:** Used to finalize and prepare software for specific versions.
- **Upstream First Policy:** Merge changes into the main branch first and then cherry-pick them into the release branch to avoid inconsistencies.
- **Tagging:** Create a new tag for each release to mark the version clearly.
- **Stable Branch:** Maintains a reference to the latest stable version, and may be used for hotfixes.
- **Production Branch:** Not always necessary if the release and stable branches serve the purpose.

This approach ensures that your releases are well-managed, bug fixes are consistently applied, and your versioning is clear and organized.

![alt text](Images/image-1.png)

![alt text](Images/image-2.png)

![alt text](Images/image-3.png)

In GitLab, an **Epic** is a high-level feature or large piece of work that is typically broken down into smaller, more manageable issues or tasks. Epics are used to organize and track work across multiple projects or issues and are particularly useful for managing large projects or features that span several milestones or iterations.

### Key Features of Epics in GitLab

1. **High-Level Organization:**

   - Epics provide a way to group related issues and merge requests under a single umbrella. This helps in organizing work at a broader level than individual issues or merge requests.

2. **Cross-Project Visibility:**

   - Epics can span across different projects within the same group. This is useful for large projects that involve multiple repositories.

3. **Tracking Progress:**

   - GitLab allows you to track the progress of an Epic by showing how many issues or merge requests are completed versus those that are still in progress. This provides a high-level view of the status of the larger feature or goal.

4. **Hierarchical Structure:**

   - Epics can be organized into a hierarchy where an Epic can have related child Epics. This hierarchical structure helps in managing complex projects with multiple layers of work.

5. **Roadmaps:**

   - GitLab provides a roadmap view where you can see the timeline of Epics, helping to visualize and plan the overall progress of large projects.

6. **Issue Linking:**
   - Issues and merge requests can be linked to an Epic, providing context and ensuring that all related work is tracked together.

When a merge request is created, it is marked as a draft by default. The Draft keyword in the title of the merge request indicates that the merge is currently a draft. A draft merge cannot be merged until it is marked as ready. This helps to prevent accidental merges.

### **Understanding GitLab CI/CD**

**Continuous Integration (CI)** and **Continuous Delivery (CD)** are fundamental practices in modern software development that aim to improve code quality, streamline workflows, and accelerate delivery cycles. Here’s a detailed explanation of each practice and how they work together in GitLab CI/CD:

### **Continuous Integration (CI)**

1. **Definition and Purpose:**

   - **Continuous Integration (CI)** is a development practice where code changes are frequently integrated into a shared repository. The key idea is to merge code changes from multiple developers into a central repository several times a day.
   - **Purpose:** CI helps in identifying integration issues early, improving code quality, and fostering collaboration among team members. It ensures that code changes do not break the existing codebase and that the software remains functional and stable.

2. **Process:**

   - **Code Commit:** Developers commit their code changes to a shared repository.
   - **Automated Build:** Each commit triggers an automated build process to compile the code and ensure that it integrates correctly with the existing codebase.
   - **Automated Testing:** Automated tests are run to validate the changes. This includes unit tests, integration tests, and other types of testing to ensure code correctness and stability.
   - **Feedback:** Developers receive feedback on their changes, allowing them to address issues quickly before the code is integrated into the main branch.

3. **Benefits:**
   - **Early Issue Detection:** CI helps catch integration problems and bugs early in the development cycle.
   - **Improved Collaboration:** By frequently integrating code, team members can collaborate more effectively and avoid conflicts.
   - **Maintained Code Quality:** Automated testing ensures that the codebase remains reliable and stable.

### **Continuous Delivery (CD)**

1. **Definition and Purpose:**

   - **Continuous Delivery (CD)** extends the principles of CI to automate the delivery of code changes to production or staging environments. The goal is to ensure that software is always in a deployable state and that deployments can occur frequently and reliably.
   - **Purpose:** CD streamlines the release process, making it easier to deploy new features, respond to customer feedback, and fix bugs promptly.

2. **Process:**

   - **Automated Deployment:** After successful integration and testing, code changes are automatically deployed to a staging environment. This environment closely mirrors the production environment.
   - **Manual Approval (Optional):** Depending on the configuration, a manual approval step may be required before deploying changes to the production environment.
   - **Production Deployment:** Once approved, changes are deployed to the production environment, where they are made available to end users.

3. **Benefits:**
   - **Frequent Releases:** CD allows for frequent and reliable releases of new features, enhancements, and fixes.
   - **Reduced Risk:** By automating deployment and testing processes, CD reduces the risk associated with manual deployments and ensures that software is always in a releasable state.
   - **Faster Response:** Teams can respond more quickly to user feedback and market demands.

![alt text](Images/image.png)

# Anatomy of a CI/CD Pipeline

This is an example of a pipeline graph that shows what the CI/CD build looks like. It lets you see how a set of one or more jobs are executed in the stages you define in the YAML file for the pipeline.

![alt text](Images/image4.png)

![alt text](Images/image5.png)

# Git Command

### Getting & Creating Projects

| Command                                                           | Description                                |
| ----------------------------------------------------------------- | ------------------------------------------ |
| `git init`                                                        | Initialize a local Git repository          |
| `git clone ssh://git@github.com/[username]/[repository-name].git` | Create a local copy of a remote repository |

### Basic Snapshotting

| Command                            | Description                                       |
| ---------------------------------- | ------------------------------------------------- |
| `git status`                       | Check status                                      |
| `git add [file-name.txt]`          | Add a file to the staging area                    |
| `git add -A`                       | Add all new and changed files to the staging area |
| `git commit -m "[commit message]"` | Commit changes                                    |
| `git rm -r [file-name.txt]`        | Remove a file (or folder)                         |

### Branching & Merging

| Command                                              | Description                                             |
| ---------------------------------------------------- | ------------------------------------------------------- |
| `git branch`                                         | List branches (the asterisk denotes the current branch) |
| `git branch -a`                                      | List all branches (local and remote)                    |
| `git branch [branch name]`                           | Create a new branch                                     |
| `git branch -d [branch name]`                        | Delete a branch                                         |
| `git push origin --delete [branch name]`             | Delete a remote branch                                  |
| `git checkout -b [branch name]`                      | Create a new branch and switch to it                    |
| `git checkout -b [branch name] origin/[branch name]` | Clone a remote branch and switch to it                  |
| `git branch -m [old branch name] [new branch name]`  | Rename a local branch                                   |
| `git checkout [branch name]`                         | Switch to a branch                                      |
| `git checkout -`                                     | Switch to the branch last checked out                   |
| `git checkout -- [file-name.txt]`                    | Discard changes to a file                               |
| `git merge [branch name]`                            | Merge a branch into the active branch                   |
| `git merge [source branch] [target branch]`          | Merge a branch into a target branch                     |
| `git stash`                                          | Stash changes in a dirty working directory              |
| `git stash clear`                                    | Remove all stashed entries                              |

### Sharing & Updating Projects

| Command                                                                           | Description                                                 |
| --------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| `git push origin [branch name]`                                                   | Push a branch to your remote repository                     |
| `git push -u origin [branch name]`                                                | Push changes to remote repository (and remember the branch) |
| `git push`                                                                        | Push changes to remote repository (remembered branch)       |
| `git push origin --delete [branch name]`                                          | Delete a remote branch                                      |
| `git pull`                                                                        | Update local repository to the newest commit                |
| `git pull origin [branch name]`                                                   | Pull changes from remote repository                         |
| `git remote add origin ssh://git@github.com/[username]/[repository-name].git`     | Add a remote repository                                     |
| `git remote set-url origin ssh://git@github.com/[username]/[repository-name].git` | Set a repository's origin branch to SSH                     |

### Inspection & Comparison

| Command                                    | Description                    |
| ------------------------------------------ | ------------------------------ |
| `git log`                                  | View changes                   |
| `git log --summary`                        | View changes (detailed)        |
| `git log --oneline`                        | View changes (briefly)         |
| `git diff [source branch] [target branch]` | Preview changes before merging |

# Head in Git

![alt text](Images/image7.png)

The `git checkout HEAD^` command is used to check out the commit immediately before the current commit. Here's a breakdown of what this command does and how it works:

### Understanding `HEAD^`

- **`HEAD`**: Refers to the current commit your working directory is based on.
- **`HEAD^`**: Refers to the parent commit of `HEAD`. In Git, `HEAD^` is shorthand for `HEAD~1`, which means "one commit before the current commit." If you want to go further back, you can use `HEAD^^` (or `HEAD~2`), `HEAD~~~` (or `HEAD~3`), and so on.

### Using `git checkout HEAD^`

1. **Checkout the Parent Commit**:

   ```bash
   git checkout HEAD^
   ```

   This command checks out the parent commit of the current commit, placing your working directory into a "detached HEAD" state.

2. **Viewing Changes**: Once checked out, you can inspect files and see the state of the repository at the parent commit.

### Example Scenario

Imagine your commit history looks like this:

```
A -- B -- C -- D (HEAD)
```

If you run `git checkout HEAD^`, you will switch to commit `C`.

### Working with Detached HEAD State

- **Inspect Files**: You can view the files as they were in the parent commit.
- **Make Changes**: If you make changes and want to keep them, you should create a new branch:
  ```bash
  git checkout -b new-branch-name
  ```
- **Return to the Branch**: To go back to the latest commit on your branch:
  ```bash
  git checkout main
  ```
  Replace `main` with whatever branch you were on before.

### Important Notes

- **Detached HEAD State**: In this state, any new commits won’t be saved to a branch unless you explicitly create a new branch or otherwise integrate them.
- **Recovery**: If you make changes in the detached HEAD state and don’t create a new branch, those changes might be lost when switching to another commit or branch.

Using `HEAD^` is useful for viewing or reverting to previous states in your repository, but remember to manage your commits and branches carefully to avoid losing work.

# Branch Forcing

![alt text](Images/image8.png)

### `git reset`

The `git reset` command is used to move the current branch's HEAD to a specified state, and it can also modify the staging area and working directory. There are three primary forms of `git reset`:

1. **Soft Reset (`--soft`)**:

   - **Usage**: `git reset --soft <commit>`
   - **Effect**: Moves the HEAD to the specified commit, but keeps changes in the index (staging area) and working directory. This means changes made after the specified commit are still staged and can be committed again.
   - **Example**:
     ```bash
     git reset --soft HEAD~1
     ```
     This command will move HEAD to the previous commit while keeping your changes staged.

2. **Mixed Reset (default)**:

   - **Usage**: `git reset <commit>`
   - **Effect**: Moves the HEAD to the specified commit and updates the staging area to match it, but does not modify the working directory. This effectively unstages any changes made after the specified commit but leaves the changes in your working directory.
   - **Example**:
     ```bash
     git reset HEAD~1
     ```
     This command will move HEAD to the previous commit and unstage changes made after that commit, but the changes will still be in your working directory.

3. **Hard Reset (`--hard`)**:
   - **Usage**: `git reset --hard <commit>`
   - **Effect**: Moves the HEAD to the specified commit, updates the staging area, and modifies the working directory to match the commit. All changes in the working directory and staging area are discarded.
   - **Example**:
     ```bash
     git reset --hard HEAD~1
     ```
     This command will reset your branch to the previous commit and discard all changes in your working directory and staging area.

### `git revert`

The `git revert` command is used to create a new commit that undoes the changes made by a previous commit. Unlike `git reset`, `git revert` does not alter the commit history but instead adds a new commit that effectively reverses the changes.

- **Usage**: `git revert <commit>`
- **Effect**: Creates a new commit that reverses the changes introduced by the specified commit. This is useful for undoing changes in a shared history without rewriting the commit history.
- **Example**:
  ```bash
  git revert a1b2c3d4
  ```
  This command will create a new commit that reverses the changes made in commit `a1b2c3d4`.

### Key Differences

- **History Modification**:

  - `git reset` can alter commit history, especially with `--hard` or `--soft`, which can affect collaborators if pushed to a shared repository.
  - `git revert` does not change commit history; it creates a new commit that undoes the changes, making it safer for shared branches.

- **Usage Context**:

  - Use `git reset` for local changes, when you want to undo or redo commits before they’re shared with others.
  - Use `git revert` for undoing changes in a way that is safe for shared branches, as it preserves commit history.

- **Effect on Working Directory**:
  - `git reset --hard` will affect your working directory and discard changes.
  - `git revert` will leave your working directory as is but adds a new commit to reverse the changes.

### Summary

- **`git reset`**: Alters branch history and can modify the working directory. Use for local changes and history adjustments.
- **`git revert`**: Creates a new commit to reverse changes without altering commit history. Use for undoing changes safely in shared repositories.

### Role Hierarchy Overview

![alt text](Images/image9.png)

In GitLab, roles and permissions are crucial for managing access and controlling what users can do within projects and groups. Here's a detailed explanation of the role hierarchy and how it works when a user is assigned multiple roles:

When managing users in GitLab, roles are assigned to determine the level of access and control a user has within a project or group. GitLab uses a hierarchical system where different roles have varying levels of permissions.

#### **Project vs. Group Roles**

- **Project Roles**: Define permissions specifically for a single project.
- **Group Roles**: Define permissions within a group that can contain multiple projects. These roles can apply to all projects within the group.

### Hierarchical Role System

1. **Role Levels**:

   - **Guest**: Limited access, mostly read-only. Can view issues, merge requests, and some other elements but cannot make changes.
   - **Reporter**: Can view and comment on issues, view code, and see most aspects of the project but cannot make changes.
   - **Developer**: Can push code, manage issues, and perform other development-related tasks. Has more permissions than Reporter.
   - **Maintainer**: Can manage project settings, handle project configuration, and have broad control over the project. Higher level than Developer.
   - **Owner**: (For groups) Has the highest level of control over a group and its projects. Owners can change group settings, manage members, and more.

2. **Permissions Hierarchy**:
   - **Project Roles**: When a user is assigned a role at the project level, their permissions are confined to that specific project.
   - **Group Roles**: When a user is assigned a role at the group level, it applies to all projects within the group. If a project has its own roles defined, the group role will apply to all projects under the group by default.

### When a User is Added to Both a Project and a Group

If a user is added to both a group and a project with different roles, GitLab uses the higher role to determine their effective permissions. Here’s how it works:

1. **Role Assignment**:

   - **Group Role**: If a user is assigned a role (e.g., Developer) at the group level, this role will apply to all projects within that group.
   - **Project Role**: If the same user is also assigned a different role (e.g., Maintainer) at the project level, the project-specific role takes precedence.

2. **Effective Permissions**:
   - The user’s permissions are governed by the highest role they hold in any of the contexts where they are assigned. For example, if a user has a Developer role at the group level and a Maintainer role at the project level, they will have the permissions associated with the Maintainer role in that project.

### Example

Consider a user who is assigned:

- **Developer** role in a group.
- **Maintainer** role in a specific project within that group.

In this case:

- **For the group**: The user will have Developer-level permissions across all projects in the group.
- **For the specific project**: The user will have Maintainer-level permissions due to the project-specific role, which overrides the group-level role for this particular project.

### Summary

- **Group Roles**: Apply to all projects within the group and define default permissions.
- **Project Roles**: Apply specifically to individual projects and can override group-level permissions.
- **Role Precedence**: When a user has roles at both the group and project levels, the higher role’s permissions apply in the specific context where the higher role is assigned.

Understanding this hierarchy helps ensure that users have appropriate access levels and that permissions are correctly managed across both group-wide and project-specific contexts in GitLab.

# Milestones

Milestones
Milestones in GitLab are a way to track issues and merge requests created to achieve a broader goal in a certain period of time. Milestones allow you to organize issues and merge requests into a cohesive group, with an optional start date and an optional due date.

For example, if you have a lot of issues related to a specific deliverable or goal, you can create a milestone and assign all of the issues to it.

Key features/functions

You can assign both issues and merge requests to milestones
Everything assigned to the same milestone shares the same start date and end date
Milestones can exist at the project or group level
The milestone view also contains a burndown and burnup chart showing the progress of completing a milestone

# Iterations

Iterations are a way to track issues over a period of time. This allows teams to track velocity and volatility metrics. For tracking over different time periods, you can use iterations milestones. You can create and manage various iteration cadences.

For example, you can use:

Milestones for Program Increments, which span 8-12 weeks.
Iterations for Sprints, which span 2 weeks.

Key features/functions

You can consider an iteration like a sprint and assign issues to your iterations
Iterations are at the group level only and groups can have only 1 active iteration at a time
Iterations are grouped into iteration cadences
Iterations require start and end dates
Iteration date ranges cannot overlap within an iteration cadence
The iteration detail page shows you overall % complete as well as burndown and burnup charts

![alt text](Images/image10.png)

![alt text](Images/image11.png)

# PIPELINE

A pipeline is made of multiple stages , and stages consists of one or multiple job and the job are executed by the runner that makes job complete and hand it over to the Gitlab.

<!-- Gitlab pipeline details  -->

<!-- ////////////////////////// -->

# Docker Image

A Docker image is a lightweight, standalone, and executable package that includes everything needed to run a piece of software. This includes the code, runtime, libraries, environment variables, and configuration files.

In more detail:

- **Layered Structure:** Docker images are made up of layers. Each layer represents a set of file changes or additions and is built on top of previous layers. This layered structure allows for efficient use of disk space and makes it easier to distribute and update images.

- **Immutability:** Once a Docker image is created, it doesn’t change. This immutability ensures that the software runs the same way regardless of where it is deployed, leading to consistent environments.

- **Portability:** Docker images can be run on any system that has Docker installed, regardless of the underlying operating system or hardware. This portability is one of the main benefits of using Docker.

- **Reusability:** Since Docker images can be built from a base image (like an official operating system or language runtime image) and then customized, they promote reuse and sharing of common configurations and dependencies.

- **Dockerfile:** The Docker image is typically built from a `Dockerfile`, which is a text file containing instructions on how to construct the image. The `Dockerfile` specifies the base image, copies files, installs dependencies, and sets up the environment for the application.

Overall, Docker images help streamline development, testing, and deployment processes by providing a consistent environment across different stages and platforms.

# Services

The services keyword allows us to augment our base image with an additional image if one container isn't enough. This additional image is used to create another container, which is available for the first container. These two containers have access to one another and can communicate when running the job.

The service image can run any application, but the most common use case is to run a database container as we've done in the example above by adding a Postgres container.

In GitLab, artifacts and cache are two important concepts used to optimize the CI/CD pipeline and improve build efficiency.

### **Artifacts and Cache**

Artifacts in GitLab are files or directories created by a job that you want to save and use in later stages of your pipeline or share with other jobs. Artifacts are typically generated by build or test jobs and can be used for a variety of purposes:

- **Storing Build Results:** For example, if you have a build job that generates a compiled binary or a set of reports, these files can be saved as artifacts.
- **Passing Data Between Jobs:** Artifacts can be used to share data between different jobs in a pipeline. For instance, you might need to pass build outputs to a deployment job.

**Configuration Example:**

Here’s an example of how you might configure artifacts in a `.gitlab-ci.yml` file:

```yaml
build:
  stage: build
  script:
    - make build
  artifacts:
    paths:
      - build/
    expire_in: 1 week
```

In this example, the `build` job generates files in the `build/` directory, which are then stored as artifacts. The `expire_in` field specifies how long the artifacts should be kept before being automatically deleted.

### **Cache**

Cache in GitLab is used to speed up the execution of jobs by reusing data from previous jobs. Caching is typically used for dependencies or other files that are expensive to generate or download repeatedly.

**Usage Examples:**

- **Dependency Caching:** You can cache dependencies (like npm modules or Maven dependencies) to avoid re-downloading them on every pipeline run.
- **Build Caching:** Cache build directories to speed up incremental builds.

**Configuration Example:**

Here’s an example of how to configure caching in a `.gitlab-ci.yml` file:

```yaml
build:
  stage: build
  script:
    - npm install
    - npm run build
  cache:
    key: ${CI_COMMIT_REF_SLUG}
    paths:
      - node_modules/
```

In this example, the `node_modules/` directory is cached between builds. The `key` field ensures that the cache is specific to a particular branch or commit, which helps avoid using outdated cache data.

### **Key Differences**

- **Artifacts:** Used to store files generated by jobs and to make them available to later jobs in the pipeline. Artifacts are often used for outputs that need to be preserved beyond the lifetime of a single job.
- **Cache:** Used to speed up pipeline execution by reusing previously stored data. Caches are typically used for dependencies or build artifacts that are expensive to regenerate or download.

By using artifacts and cache effectively, you can improve the efficiency and speed of your CI/CD pipelines in GitLab.

Dependencies
Dependencies restrict which artifacts are passed to a specific job by providing a list of jobs to fetch artifacts from selectively. They are defined in the job and pass a list of all previous jobs the artifacts should be downloaded from. See below for an example YAML file with dependencies.

```yaml
build:osx:
  stage: build
  script: make build:osx
  artifacts:
    paths:
      - binaries/

build:linux:
  stage: build
  script: make build:linux
  artifacts:
    paths:
      - binaries/

test:osx:
  stage: test
  script: make test:osx
  dependencies:
    - build:osx

test:linux:
  stage: test
  script: make test:linux
  dependencies:
    - build:linux

deploy:
  stage: deploy
  script: make deploy
```

# Rules

Rules are a way to define under what conditions a job should run. Have a deploy job that should only be run on a particular branch? Want to skip a job if no changes are made to a corresponding file? Need to delay when a job runs to avoid peak hours? The rules syntax in your YAML file can be configured to handle all of these use cases. Order matters

Rules are evaluated in order until the first match, so order matters. When the first condition is met, the job is either included or excluded from the pipeline depending on the configuration.

Example 1: Only Deploy from Main Branch
This deploy job will always run on the main branch. Otherwise, it will never run.

```yaml
pseudo-deploy:
  stage: deploy
  script:
    - command deploy_review
  rules:
    - if: '$CI_COMMIT_REF_NAME == "main"'
      when: always
    - when: never
```

Close Example 2: Triggered by a Merge Request
This conditional rule ensures that a pipeline only runs when a merge request event is triggered:

```yaml
job:
  script: "echo Hello, Rules!"
  rules:
    - if: ‘$CI_PIPELINE_SOURCE == “merge_request_event”’
```

Close Example 3: Delayed Job Start & Allowed Failure
This job will run 3 hours after triggered and will be allowed to fail (will not prevent further stages from firing):

```yaml
docker build:
  script: docker build -t my-image:$CI_COMMIT_REF_SLUG .
  rules:
    - if: '$CI_COMMIT_BRANCH == "main"'
    when: delayed
    start_in: '3 hours'
    allow_failure: true
```

Close Example 4: Workflow Rules
This pipeline will not run if the commit message ends with “-wip”. It also will not run if it was triggered by a tag being applied. Otherwise, this pipeline will run.

```yaml
workflow:
  rules:
   - if: $CI_COMMIT_MESSAGE =~ /-wip$/
      when: never
    - if: $CI_COMMIT_TAG
   when: never
    - when: always
<<<<<<< HEAD
```

# Needs

The needs keyword enables executing jobs out-of-order, allowing you to implement a directed acyclic graph (DAG) in your CI configuration.

This lets you run some jobs without waiting for other ones, disregarding stage ordering so you can have multiple stages running concurrently. You can ignore stage ordering and run some jobs without waiting for others to complete. Jobs in multiple stages can run concurrently. See below for an example YAML with needs utilized.

```yaml
linux:build:
  stage: build

mac:build:
  stage: build

lint:
  stage: test
  needs: []

linux:rspec:
  stage: test
  needs: ["linux:build"]

mac:rubocop:
  stage: test
  needs: ["mac:build"]

production:
  stage: deploy
```

# Reusable Template

Creating a reusable pipeline in GitLab is a great way to streamline your CI/CD processes and ensure consistency across projects. In GitLab, you can create reusable pipelines by using templates, including predefined jobs, or defining custom pipeline configurations that can be included in multiple `.gitlab-ci.yml` files.

Here's how you can create a reusable pipeline in GitLab:

### 1. **Create a Template Repository**

- Create a repository that will hold your reusable pipeline definitions.
- In this repository, you can define your pipeline stages, jobs, and variables.

### 2. **Define Reusable Jobs in the Template**

- In your template repository, create a `.gitlab-ci.yml` file where you define the jobs you want to reuse.

Example:

```yaml
# .gitlab-ci.yml in the template repository
.build_job_template:
  script:
    - echo "Running the build job"
    - make build

.test_job_template:
  script:
    - echo "Running tests"
    - make test

.deploy_job_template:
  script:
    - echo "Deploying application"
    - make deploy
```

Here, `.build_job_template`, `.test_job_template`, and `.deploy_job_template` are defined as hidden jobs (jobs prefixed with a dot) that are not executed directly but can be included in other pipelines.

### 3. **Include the Template in Other Projects**

- In the `.gitlab-ci.yml` of your other projects, you can include the jobs defined in the template repository.

Example:

```yaml
include:
  - project: "namespace/template-repository"
    file: "/.gitlab-ci.yml"

stages:
  - build
  - test
  - deploy

build:
  extends: .build_job_template

test:
  extends: .test_job_template

deploy:
  extends: .deploy_job_template
```

Here, `include` is used to pull the `.gitlab-ci.yml` from the template repository, and `extends` is used to reuse the jobs defined there.

### 4. **Use Pipeline Variables**

- You can use pipeline variables to customize the behavior of the reusable jobs.

Example:

```yaml
variables:
  BUILD_ENV: "production"

build:
  extends: .build_job_template
  script:
    - echo "Building for $BUILD_ENV"
    - make build
```

The `BUILD_ENV` variable can be customized per project or pipeline.

### 5. **Test and Maintain the Template**

- Test the reusable pipeline by running it in different projects.
- Keep the template repository updated and version-controlled to maintain consistency across all pipelines that use it.

### Benefits of Reusable Pipelines:

- **Consistency**: Ensures that the same steps are followed in different projects.
- **Maintainability**: Changes can be made in one place (the template repository) and automatically propagate to all pipelines that include the template.
- **Efficiency**: Reduces duplication of code and configuration, making your pipelines easier to manage.

This approach allows you to create scalable and maintainable CI/CD pipelines across multiple projects in GitLab.
