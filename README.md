# What is power amend?

A shell script to amend the non-HEAD commit. The usage totally follows "git commit --amend":

- Staged files will be amended to the target commit.
- Unstaged files remain unstaged.
- Untracked files remain untracked.
- You will stay on the same branch.

# Warning

- The SHA1 values from the amended commit to [HEAD] will all be changed.
- If you forgot to stage any change to amend, you can still change the commit message.

# Usage

It's just a shell script so you can download and run it or set as a custom git command (e.g. git power-amend). To have a quick try, see the following section.

# Have a quick try!
````
bash <(curl -L -s https://goo.gl/85y4bM) [revision]
````

e.g.
````
bash <(curl -L -s https://goo.gl/85y4bM) HEAD^^^
bash <(curl -L -s https://goo.gl/85y4bM) 2d161a3
````

A real world case:
````
$ bash <(curl -L -s https://goo.gl/85y4bM) HEAD^^^^^^^^
>>>> The following commits will be affected:

[HEAD]  2d161a3 Bug 1189846 Part 9: Add ability to print from the parent process with settings and progress listener. r=jimm, r=smaug
        80ef820 Bug 1189846 Part 8: Make RemotePrintJob a print progress listener forwarder. r=jimm
        3a3dd7e Bug 1189846 Part 7: Create nsPrintingProxy and PrintingParent during process initialization. r=jimm
        1153e65 Bug 1189846 Part 6: Remove GetNativeData from nsIPrintOptions. r=jimm
        8312249 Bug 1189846 Part 5: Remove displayJobProperties from nsIPrintOptions. r=jimm
        f5d114a Bug 1189846 Part 4: Remove getPrinterPrefInt from nsIPrintOptions. r=jimm
        757e385 Bug 1189846 Part 3: Remove CreatePrintSettings nsIPrintOptions and use GetNewPrintSettings instead. r=jimm
        fa0843f Bug 1189846 Part 2: Make Android CreatePrintSettings work like other OS specific ones. r=snorp
[AMEND] 3098283 Bug 1189846 Part 1: Move PrintSettings serialization into nsIPrintSettingsService. r=jimm

>>>> Only [AMEND] will be amended but all will have new SHA1 value.
>>>> History is going to be rewritten. Continue? [y/n] y
>>>> Working branch is power-amend-test
>>>> Created backup working branch power-amend-test-backup-1a2e505e-1ceb-11e6-ae08-08606e456b8a.
>>>> Saving the fixup changes to power-amend-test-fixup-1a2e505e-1ceb-11e6-ae08-08606e456b8a ...
M	modules/libpref/init/all.js
Switched to a new branch 'power-amend-test-fixup-1a2e505e-1ceb-11e6-ae08-08606e456b8a'
[power-amend-test-fixup-1a2e505e-1ceb-11e6-ae08-08606e456b8a 3b98ac9] Temp commit for fixup.
 1 file changed, 1 insertion(+), 1 deletion(-)
>>>> Stashing the unstaged changes ...
No local changes to save
>>>> Switching back to the working branch ...
Switched to branch 'power-amend-test'
>>>> Rewinding to the revision we'd like to amend ...
HEAD is now at 3098283 Bug 1189846 Part 1: Move PrintSettings serialization into nsIPrintSettingsService. r=jimm
>>>> Cherry-picking fixup commit ...
>>>> Amending commit that we cherry-picked from power-amend-test-fixup-1a2e505e-1ceb-11e6-ae08-08606e456b8a ...
[power-amend-test 2e698f7] Bug 1189846 Part 1: Move PrintSettings serialization into nsIPrintSettingsService. r=jimm
 Author: Bob Owen <bobowencode@gmail.com>
 5 files changed, 73 insertions(+), 68 deletions(-)
>>>> Cherry-picking the untouched commits ...
[power-amend-test 0d901ec] Bug 1189846 Part 2: Make Android CreatePrintSettings work like other OS specific ones. r=snorp
 Author: Bob Owen <bobowencode@gmail.com>
 2 files changed, 3 insertions(+), 2 deletions(-)
[power-amend-test 38c0129] Bug 1189846 Part 3: Remove CreatePrintSettings nsIPrintOptions and use GetNewPrintSettings instead. r=jimm
 Author: Bob Owen <bobowencode@gmail.com>
 4 files changed, 9 insertions(+), 24 deletions(-)
[power-amend-test 8700bb7] Bug 1189846 Part 4: Remove getPrinterPrefInt from nsIPrintOptions. r=jimm
 Author: Bob Owen <bobowencode@gmail.com>
 2 files changed, 2 insertions(+), 31 deletions(-)
[power-amend-test 2c1ff55] Bug 1189846 Part 5: Remove displayJobProperties from nsIPrintOptions. r=jimm
 Author: Bob Owen <bobowencode@gmail.com>
 5 files changed, 55 deletions(-)
[power-amend-test a3f185e] Bug 1189846 Part 6: Remove GetNativeData from nsIPrintOptions. r=jimm
 Author: Bob Owen <bobowencode@gmail.com>
 2 files changed, 12 deletions(-)
[power-amend-test faf9c6e] Bug 1189846 Part 7: Create nsPrintingProxy and PrintingParent during process initialization. r=jimm
 Author: Bob Owen <bobowencode@gmail.com>
 4 files changed, 33 insertions(+), 11 deletions(-)
[power-amend-test 4aa6145] Bug 1189846 Part 8: Make RemotePrintJob a print progress listener forwarder. r=jimm
 Author: Bob Owen <bobowencode@gmail.com>
 12 files changed, 194 insertions(+), 4 deletions(-)
[power-amend-test bd66080] Bug 1189846 Part 9: Add ability to print from the parent process with settings and progress listener. r=jimm, r=smaug
 Author: Bob Owen <bobowencode@gmail.com>
 12 files changed, 266 insertions(+), 30 deletions(-)
>>>> Restoring un-staged changes ...
No stash found.
>>>> Cleaning up the temp branches ...
Deleted branch power-amend-test-fixup-1a2e505e-1ceb-11e6-ae08-08606e456b8a (was 3b98ac9).
Deleted branch power-amend-test-backup-1a2e505e-1ceb-11e6-ae08-08606e456b8a (was 2d161a3).

````
