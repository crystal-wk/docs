# Source: https://github.com/bytedance/deer-flow/blob/main/deer-flow.code-workspace

### Uh oh!

There was an error while loading. [Please reload this page]().

[bytedance](https://github.com/bytedance) / **[deer-flow](https://github.com/bytedance/deer-flow)** Public

- [Notifications](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow) You must be signed in to change notification settings
- [Fork 10.9k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)
- [Star 79.8k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)

 ## FilesExpand file tree

main

/

# deer-flow.code-workspace

Copy path

Blame

More file actions

Blame

More file actions

## Latest commit

[![foreleven](https://avatars.githubusercontent.com/u/4785594?v=4&size=40)](https://github.com/foreleven) [foreleven](https://github.com/bytedance/deer-flow/commits?author=foreleven)

[feat: Add metadata and descriptions to various documentation pages in…](https://github.com/bytedance/deer-flow/commit/44d9953e2e2f4f2993660ecb191be86ed89e608a)

Open commit details

Apr 26, 2026

[44d9953](https://github.com/bytedance/deer-flow/commit/44d9953e2e2f4f2993660ecb191be86ed89e608a) · Apr 26, 2026

## History

[History](https://github.com/bytedance/deer-flow/commits/main/deer-flow.code-workspace)

Open commit details

History

47 lines (47 loc) · 1.13 KB

## FilesExpand file tree

main

/

# deer-flow.code-workspace

Copy path

Top

## File metadata and controls

- Code

- Blame

47 lines (47 loc) · 1.13 KB

[Raw](https://github.com/bytedance/deer-flow/raw/refs/heads/main/deer-flow.code-workspace)

Copy raw file

Download raw file

Open symbols panel

Edit and raw actions

{ "folders": \[ { "path": "." } \], "settings": { "js/ts.tsdk.path": "frontend/node\_modules/typescript/lib", "python-envs.pythonProjects": \[ { "path": "backend", "envManager": "ms-python.python:venv", "packageManager": "ms-python.python:pip", "workspace": "deer-flow" } \] }, "launch": { "version": "0.2.0", "configurations": \[ { "name": "Debug Lead Agent", "type": "debugpy", "request": "launch", "program": "${workspaceFolder}/backend/debug.py", "console": "integratedTerminal", "cwd": "${workspaceFolder}/backend", "env": { "PYTHONPATH": "${workspaceFolder}/backend" }, "justMyCode": false }, { "name": "Debug Lead Agent (justMyCode)", "type": "debugpy", "request": "launch", "program": "${workspaceFolder}/backend/debug.py", "console": "integratedTerminal", "cwd": "${workspaceFolder}/backend", "env": { "PYTHONPATH": "${workspaceFolder}/backend" }, "justMyCode": true } \] } }

1

2

3

4

5

6

7

8

9

10

11

12

13

14

15

16

17

18

19

20

21

22

23

24

25

26

27

28

29

30

31

32

33

34

35

36

37

38

39

40

41

42

43

44

45

46

47

{

"folders": \[

{

"path": "."

}

\],

"settings": {

"js/ts.tsdk.path": "frontend/node\_modules/typescript/lib",

"python-envs.pythonProjects": \[

{

"path": "backend",

"envManager": "ms-python.python:venv",

"packageManager": "ms-python.python:pip",

"workspace": "deer-flow"

}

\]

},

"launch": {

"version": "0.2.0",

"configurations": \[

{

"name": "Debug Lead Agent",

"type": "debugpy",

"request": "launch",

"program": "${workspaceFolder}/backend/debug.py",

"console": "integratedTerminal",

"cwd": "${workspaceFolder}/backend",

"env": {

"PYTHONPATH": "${workspaceFolder}/backend"

},

"justMyCode": false

},

{

"name": "Debug Lead Agent (justMyCode)",

"type": "debugpy",

"request": "launch",

"program": "${workspaceFolder}/backend/debug.py",

"console": "integratedTerminal",

"cwd": "${workspaceFolder}/backend",

"env": {

"PYTHONPATH": "${workspaceFolder}/backend"

},

"justMyCode": true

}

\]

}

}