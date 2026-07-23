# collaborate with others on a repo, resolve merge conflicts, and create your first pull request 
============================================================================================  
### 🧗 Step 1: The Fork & Clone
1. Developer A creates a public repository named `git-adventure` and add a simple `README.md` 
2. Developer A invite Developer B to collaborate by going to **Settings > Collaborators** 
3. Developer B accept the invite, then open his terminal and clone the repository locally
```
git clone https://github.com/developera/git-adventure.git
```   
============================================================================================    
### 🌿 Step 2: Branching Out (Parallel Universes)
1. Developer B create and switch to new branch to work on the theme of the adventure
```
git switch -c theme/conflicted-pull
```
2. open the `README.md` file in his code editor
3. underneath the title, Developer B add _saving the pull request_ on Line 3
4. Developer B save the file, commit his changes, and push his new branch to GitHub   
```
git add README.md
git commit -m "theme: add saving the pull..."
git push origin theme/conflicted-pull
```
============================================================================================    
### 🚨 Step 3: Creating a Conflict
_To understand how conflicts happen, Developer A is going to accidentally change the exact same line of code on the main branch._   
1. Developer A open the local copy of the repository (stay on the main branch)
2. Open the ` README.md` file in their file editor.
3. On **Line 3**, added _communicate better_
4. Commit and push this change directly to remote main branch
```
git add README.md
git commit -m "theme: avoid conflict"
git push origin main
```
============================================================================================      
### 🔀 Step 4: Syncing & Clashing   
Developer B is ready to bring Developer A's latest update into their theme branch before making a pull Request   
1. Developer B in his terminal fetch and pull the latest changes from Developer A's main branch into their active theme branch
```
git pull origin main
```
2. **Boom!** terminal will output a warning: `CONFLICT (content): Merge conflict in README.md`. Git has paused time until you fix it.

============================================================================================     

### ⚔️ Step 5: Resolving the Conflict   
1. Developer B open README.md in their text editor. he will see Git's conflict markers
```
<<<<<<< HEAD
You stand before massive, golden castle gates.
=======
You wake up in a dark, eerie dungeon.
>>>>>>> main
```
2. Developer B talk to Developer A and decided how to combine the theme
3. Developer B edits the file to delete the markers (`<<<<<<<`, `=======`, `>>>>>>>`) and combine the text into a coherent theme (_communicate to save pull request_).
4. Save the file, then tell Git the conflict is resolved by staging and committing it
```
git add README.md
git commit -m "fix: resolved theme tag"
git push origin theme/conflicted-pull
```   
============================================================================================         
### 🚀 Step 6: The Pull Request   
1. Developer B go to their shared repository on GitHub
2. Click the green **"Compare & Pull request"** button that popped up for theme/conflicted-pull.
3. Give a Title to the PR
4. Add description
5. Click **"Create pull request"**. Developer A can now review, leave comment, and smash the **Merge pull request** button!   
   

⬅️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️➡️   
   

# Next step after getting a pull request   

### 📚 Review the Code and Description   
- **Read the summary:** Check the PR description to understand what changes were made and why.
- **Inspect the files:** Click on the **"Files changed"** tab to see a side-by-side comparison of the old code and the new code.
- **Look for quality:** Check for bugs, formatting issues, security concerns, or a lack of comments.    
   
### 🔬 Verify Automated Checks (CI/CD)   
   

### 🧪 Test Locally (Optional but Recommended)   
- **Pull the branch:** If it is a complex feature, download their specific branch to your computer.
- **Run the app:** Test the feature locally to ensure it doesn't break existing features or cause unexpected bugs.  
   
   - **Method 1:** Using the GitHub CLI
        - Check out the PR directly:
        ```
        gh pr check <PR NUMBER>
        ```   
        _This command automatically fetches the remote branch, creates a local branch matching the PR name, and switches you right into it. You are now ready to test the code._  

   - **Method 2:** Using Standard Git Commands  
     
        **Option A: If the PR is from a branch inside your own repository**
        If a team member made the PR from a branch within your main repository, just fetch and switch to it:  
          
        1. fetch all remote branches
        ```
        git fetch origin
        ```  
          
        2. Switch to the PR's branch   
        ```
        git checkout <BRANCH_NAME>
        ```   
           
        **Option B: If the PR is from a "Fork" (External Contributor)**   
        If an outside contributor forked your repository, you need to pull their specific PR reference number into a temporary local branch:  
          
        1. Fetch the specific PR data:   
        ```
        git fetch origin pull/<PR_NUMBER>/head:pr-<PR_NUMBER>
        ```   
        _(e.g., git fetch origin pull/42/head:pr-42)_

        2. Switch to that new local PR branch:   
        ```
        git checkout pr-<PR_NUMBER>
        ```
    _Once you are finished testing, switch back to your main branch using git checkout main._
   

### 🔀 Merge the Pull Request   
Once you are satisfied and all tests pass, click the **"Merge pull request"** button. You generally have three merging choices:
- **Create a merge commit:** Combines all history exactly as it happened (best for preserving detailed commit history).
- **Squash and merge:** Combines all of the PR's commits into one single, clean commit (best for keeping the main branch history tidy).
- **Rebase and merge:** Applies the PR commits directly on top of the main branch without a merge commit.  
   

### 🧹 Clean Up   
- **Delete the branch:** After a successful merge, click the button to delete the feature branch to keep your repository clean.
- **Close issues:** If the PR included a keyword like "Closes #12", the corresponding issue will close automatically.
