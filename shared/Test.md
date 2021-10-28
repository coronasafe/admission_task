## Run Automated Tests

### 1. Install Node.js

You need to have npm installed in your computer for this problem. It comes with Node.js and you can get it by installing Node from https://nodejs.org/en/

### 2. Install dependencies

Run `npm install` to install all dependencies.

### 3. Create Create symbolic link to the executable file

#### On Windows

To create a symbolic link on Windows, you'll need to run either the Windows Command Prompt, or Windows Powershell **with administrator privileges**. To do so, right-click on the icon for Command Prompt, or Powershell, and choose the _"Run as Administrator"_ option.

**Command Prompt:**

```
> mklink tasks tasks.bat
```

**Powershell:**

```
> cmd /c mklink tasks tasks.bat
```

#### On \*nix:

Run the following command in your shell:

```
$ ln -s tasks.sh tasks
```

### 4. Try running tests.

Now run `npm test` and you will see all the tests failing. As you fill in each functionality, you can re-run the tests to see them passing one by one.

## A Note about `/` for Windows Users

In the following sections, you'll see many commands prefixed with `./`, or paths containing the `/` (forward-slash) character.

If you're using the Windows _Command Prompt_, then you'll need to replace `/` with `\` (back-slash) for these commands and paths to work as expected.

On Windows _Powershell_, these substitutions are not required.

## Known Issues

A few notes to help you avoid any hiccups while implementing the programming challenge:

1. If you are on Windows, you might have difficulty getting the tests to pass because of newline UTF encoding issues. If you get stuck, please [refer to the thread here](https://github.com/nseadlc-2020/package-todo-cli-task/issues/12).

2. In Windows machines, the `make` command might not exist and can prevent you from running the tests. This can be fixed [by using WSL, or installing MinGW, among other options](https://stackoverflow.com/questions/32127524/how-to-install-and-use-make-in-windows).

## Specification

1. The app can be run in the console with `./tasks`.

2. The app should read from and write to a tasks.txt text file. Each task occupies a single line in this file. Each line in the file should be in this format :

   ```
   p task
   ```

   where `p` is the priority ( priority will be a number) and `task` is the task description.

   > Priority denotes how important a task is, if it is a high priority task, it should be completed earlier. Priority is denoted using an integer, the lower the number, the higher the priority.

   Here is an example file that has 2 items.

   ```
   1 Buy milk
   2 Complete the project
   ```

3. Completed tasks are writted to a completed.txt file. Each task occupies a single line in this file. Each line in the file should be in this format :

   ```
   task
   ```

   where task is the task description.

   Here is an example file that has 2 items.

   ```
   Buy milk
   Complete the project
   ```

4. Priority can be any integer _greater than_ or _equal to_ 1. 1 being the highest priority

5. If two tasks have the same priority, the task that was added first should be displayed first.

   The application must open the files tasks.txt and completed.txt from where the app is run, and not where the app is located. For example, if we invoke the app like this:

6. The files should always be sorted in order of the priority, ie, the task with the highest priority should be first item in the file.

   ```
   $ cd /path/to/plans

   $ /path/to/apps/tasks ls
   ```

   The application should look for the text files in `/path/to/plans`, since that is the user’s current directory.

## Usage

### 1. Help

Executing the command without any arguments, or with a single argument help prints the CLI usage.

```
$ ./tasks help
Usage :-
$ ./tasks add 2 hello world    # Add a new item with priority 2 and text "hello world" to the list
$ ./tasks ls                   # Show incomplete priority list items sorted by priority in ascending order
$ ./tasks del INDEX            # Delete the incomplete item with the given index
$ ./tasks done INDEX           # Mark the incomplete item with the given index as complete
$ ./tasks help                 # Show usage
$ ./tasks report               # Statistics
```

### 2. List all pending items

Use the ls command to see all the items that are not yet complete, in ascending order of priority.

Every item should be printed on a new line. with the following format

```
[index] [task] [priority]
```

Example:

```
$ ./tasks ls
1. change light bulb [2]
2. water the plants [5]
```

index starts from 1, this is used to identify a particular task to complete or delete it.

### 3. Add a new item

Use the add command. The text of the task should be enclosed within double quotes (otherwise only the first word is considered as the item text, and the remaining words are treated as different arguments).

```
$ ./tasks add 5 "the thing i need to do"
Added task: "the thing i need to do" with priority 5
```

### 4. Delete an item

Use the del command to remove an item by its index.

```
$ ./tasks del 3
Deleted item with index 3
```

Attempting to delete a non-existent item should display an error message.

```
$ ./tasks del 5
Error: item with index 5 does not exist. Nothing deleted.
```

### 5. Mark a task as completed

Use the done command to mark an item as completed by its index.

```
$ ./tasks done 1
Marked item as done.
```

Attempting to mark a non-existed item as completed will display an error message.

```
$ ./tasks done 5
Error: no incomplete item with index 5 exists.
```

### 6. Generate a report

Show the number of complete and incomplete items in the list. and the complete and incomplete items grouped together.

```
$ ./tasks report
Pending : 2
1. this is a pending task [1]
2. this is a pending task with priority [4]

Completed : 3
1. completed task
2. another completed task
3. yet another completed task
```