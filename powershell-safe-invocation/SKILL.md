---
name: powershell-safe-invocation
description: Write, run, and troubleshoot PowerShell safely on Windows. Use for native executable invocation, quoted paths, argument escaping, PowerShell 5.1 versus 7 compatibility, Start-Process, multiline scripts, and filesystem mutations.
---

# PowerShell safe invocation

Prefer the simplest invocation that preserves argument boundaries and produces reliable errors. Read [reference.md](reference.md) for uncommon cases and complete examples.

## Select the shell

- Use `pwsh.exe` for PowerShell 7 unless Windows PowerShell 5.1 is required.
- Remember that `powershell.exe` is Windows PowerShell 5.1.
- Verify `$PSVersionTable.PSVersion`, command syntax, and module availability when behavior is version-sensitive.

## Invoke native programs

Pass each native argument as a separate array item:

```powershell
$exe = 'C:\Path With Spaces\tool.exe'
$nativeArgs = @('--input', 'C:\Data Folder\input.json', '--flag')
& $exe @nativeArgs
$exitCode = $LASTEXITCODE
if ($exitCode -ne 0) { throw "$exe failed with exit code $exitCode" }
```

- Invoke executable paths stored in variables with `&`.
- Capture `$LASTEXITCODE` immediately.
- Do not use `$args` as a custom variable name.
- Do not add `cmd.exe /c` unless cmd semantics are required.
- Do not use Bash-style `\"` escaping or `Invoke-Expression`.

## Invoke cmdlets

Use `-LiteralPath` for real paths and splat nontrivial parameters:

```powershell
$ErrorActionPreference = 'Stop'
$params = @{
    LiteralPath = 'C:\Data[1]\input.txt'
    Destination = 'C:\Output'
    Force = $true
    ErrorAction = 'Stop'
}
Copy-Item @params
```

Use terminating errors for cmdlets; do not inspect `$LASTEXITCODE` after a cmdlet.

## Handle complex commands

For multiline code, nested quoting, JSON, XML, regular expressions, pipelines, non-ASCII paths, or multiple interpreter layers:

1. Write a temporary `.ps1` file with explicit encoding.
2. Run `pwsh.exe -NoLogo -NoProfile -NonInteractive -File script.ps1`.

Use single quotes for literal text and double quotes only for expansion. Avoid backtick continuation. Build JSON objects and call `ConvertTo-Json` instead of hand-escaping JSON.

## Start processes

Use `& $exe @nativeArgs` for normal foreground execution. Use `Start-Process` only for elevation, detached or hidden windows, or shell behavior. When exact argument boundaries matter in a separate process, use `ProcessStartInfo.ArgumentList`.

## Mutate files safely

Before recursive delete, move, or overwrite:

1. Resolve the intended root and target to absolute paths.
2. Verify the target is strictly inside the intended root.
3. Reject empty, root-level, missing, or unexpected targets.
4. Keep enumeration and mutation in the same PowerShell process.

Use UNC paths when mapped drives are unavailable to the current account or automation session.

## Decision order

1. PowerShell cmdlet.
2. `& $exe @nativeArgs`.
3. Temporary `.ps1` with `pwsh.exe -File`.
4. `ProcessStartInfo.ArgumentList`.
5. `Start-Process` for its special behavior.
6. `cmd.exe /c` only for cmd semantics.
