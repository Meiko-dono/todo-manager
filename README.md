## In Progress
- [ ] Rewrite the extraction logic to make removal of extracted TODOs easier.
- [ ] Test the script on more usecases.

## Problem Statement
Obsidian is great for taking notes, but not so great for tracking TODOs. The checkboxes quickly accumulate, leading to a cluttered and chaotic note with a mix of completed, half-completed and incomplete tasks. Obsidian provides no easy means to remove completed TODOs without losing any data, i.e. it lacks an automatic archiving feature.

This is where todo-manager comes in. By invoking this script, all checked TODOs are moved to a systematic archive folder, cleaning up your "TODO note" without losing any data.

## Usage
This script assumes a specific folder structure, namely:

```
├── Some Group/
│   ├── TODO.md
│   └── Archive/
│       └── YYYY/
│           └── MM/
│               └── DD/
│                   └── 001_This_was_once_the_text_of_a_todo_and_got_truncate.md
└── Some other Group/
    └── TODO.md
```

I.e. I assume the TODO is a single note called `TODO` and is under some Group. There can be arbitrary many groups and each will get its own archive folder, like in `Some Group / Archive`.

The text of a completed TODO is used for the filename of its archive and any indented content under the original TODO will get copied into the archived file. 

Example:
```
- [x] This was once the text of a todo and got truncated as the text here got a bit too long.
  - [ ] Subtask 1
  - just a note
```

The above will get archived in a file with the name as in the previous file-tree example and the content of the file would look like the following:

```
# This was once the text of a todo and got truncated as the text here got a bit too long.

- [ ] Subtask 1
- just a note
```

The `Archive` folder structure is automatically built based on the date this script was invoked. Only the `TODO.md` is a hard prerequisite. 
