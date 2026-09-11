## Problem Statement
Obsidian is great for taking notes, but not so great for tracking TODOs:

- Checkboxes quickly accumulate, cluttering the TODO note.
- There are no means to automatically archive completed TODOs.

This is where todo-manager comes in. By invoking this script, all checked TODOs are moved to a date-structured archive directory, cleaning up your active TODOs without data loss.

## Requirements

This script only relies on the python standard library. Testing was performed on v3.14, but any reasonably modern version will *probably* do.

## Usage
Before use, **make sure** you understand these rules to avoid data loss. Use at your own risk.

- This script scans a vault's subdirectories for notes named `TODO.md`.
- Any directory containing a `TODO.md` is considered a `Group`.
- For each `Group` this script creates its own `Archive`.

For more details see [the next section](#principle).

To launch the script, simply run it with the environment variable `VAULT` like:
```
VAULT=/global/path/to/my/vault note-manager
```

The above command assumes the script is discoverable through the users PATH.

## Principle
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

Finally, all completed tasks are removed from the original `TODO.md`.