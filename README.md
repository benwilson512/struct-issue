# StructIssue

This project contains a module like so:
```
defmodule StructIssue do
  def run(%__MODULE__{}), do: "yo"
end
```

You'll note that it tries to use a struct `%__MODULE__{}` even though no struct has
been defined on that module. If you just run that file via `elixir` you get the
expected (and very helpful) error message:

```
$ elixir lib/struct_issue.ex
** (CompileError) lib/struct_issue.ex:3: StructIssue.__struct__/0 is undefined, cannot expand struct StructIssue
    (stdlib) lists.erl:1354: :lists.mapfoldl/3
```

If however you run it via mix, you get a different and less helpful error message:

```
$ mix
== Compilation error on file lib/struct_issue.ex ==
** (CompileError)  deadlocked waiting on module StructIssue
    (stdlib) lists.erl:1354: :lists.mapfoldl/3


Compilation failed because of a deadlock between files.
The following files depended on the following modules:

  lib/struct_issue.ex => StructIssue
```
