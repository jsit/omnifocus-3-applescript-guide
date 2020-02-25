# OmniFocus 3 AppleScript Guide


## Index of classes, properties, commands, qualifiers

### Classes
- task[s]
- project[s]
- folder[s]
- tag[s]


### Properties

#### Task properties
- name (string)
- note (string)
- primary tag (tag) (creation only)
- tags (list of tags) (modification only)
- flagged (boolean)
- blocked (boolean)
- completed (boolean)
- creation date (date)
- start date (date)
- defer date (date)
- due date (date)

#### Project properties
- name (string)
- note (string)
- singleton action holder (boolean)
- sequential (boolean)
- creation date (date)
- start date (date)
- defer date (date)
- due date (date)

#### Folder properties
- name (string)

#### Tag properties
- name (string)


### Commands

Below, "task" means the literal string "task". "tasktype" means a reference to
an object of class "task".

- `make new (task|tag|project|folder) with properties {property:value[, property:value...]}`
- `move (tasktype|tagtype|projecttype|foldertype) to (end of (tags|projects|folders) of (tagtype|projecttype|foldertype))`
- `remove tagtype from tags of tasktype`
- `add tagtype to tags of tasktype`
- `set (tasktype|projecttype) to the parent task of tasktype`


### Qualifiers
- `(task|tag|project|folder) whose name is string`
- `(task|tag|project|folder) where its name is string`
- `flattened (tasks|tags|projects|folders)`: retrieve matching items without
having to locate them within a specific hierarchy


## Examples

```AppleScript
tell front document of application "OmniFocus"

  -- Create a new project and save to variable `theProject`
  set theProject to make new project with properties {name:"Project Name", singleton action holder: true}

  -- Create a new task and save to variable `theTask`
  set theTask to make new inbox task with properties {name:"Task Name", note:"Task Note"}

  -- Move `theTask` inside of `theProject`
  move theTask to end of tasks of theProject

  -- Create a new task directly inside `theProject`
  tell theProject
    set theOtherTask to make new task with properties {name:"Other Task Name", note:"Other Task Note"}
  end tell

  -- Create a new tag
  set newTag to make new tag with properties {name:"New Tag"}

  -- Add `newTag` to `theOthertask`
  add newTag to tags of theOtherTask

  -- Create a new task with `newTag` in Inbox
  set theThirdTask to make new inbox task with properties {name:"A Third Task", primary tag:newTag}

end tell
```


## References

The following scripts and guides were an enormous help and this guide wouldn't
be possible without them:

- https://gist.github.com/matellis/69954d4212b1a36c13aad3de4e75187e#file-things3-to-of3-applescript-L350
- https://gist.github.com/AnilRh/8a0b372ffa9c4a68d6eb
- https://colterreed.com/create-omnifocus-project-templates-with-applescript/
- https://github.com/anastasiuspernat/The-Hit-List-2-Omnifocus/blob/30e4671eb2d926ff3789e9c8bacb95c60a478e4d/%5BTHL%5D%20to%20%5BOmnifocus%5D.applescript
- https://github.com/jacobsilver2/OmniFocusDailyProjectTemplate/blob/4de69359de5aa249988361473439581c8b57d77e/dailyOmniRoutine.applescript
- https://github.com/ryuiwasaki/Omnifocus2-AppleScript/blob/2ccd777c33ad15867f6fdf5f72db8459802a44d5/Omnifocus2SyncEvernote.applescript
- https://github.com/Rahlir/OmniFocusScripts/blob/3f3ef4b0502d7e32aece5ead423d0f195778619d/Scripts/omnifocuslib.applescript
- https://gist.github.com/aderyabin/1465125
- https://gist.github.com/cdzombak/11265615
