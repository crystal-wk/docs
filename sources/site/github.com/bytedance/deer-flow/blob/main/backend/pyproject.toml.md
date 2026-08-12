# Source: https://github.com/bytedance/deer-flow/blob/main/backend/pyproject.toml

### Uh oh!

There was an error while loading. [Please reload this page]().

[bytedance](https://github.com/bytedance) / **[deer-flow](https://github.com/bytedance/deer-flow)** Public

- [Notifications](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow) You must be signed in to change notification settings
- [Fork 10.9k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)
- [Star 79.8k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)

 ## FilesExpand file tree

main

/

# pyproject.toml

Copy path

Blame

More file actions

Blame

More file actions

## Latest commit

![ajayr](https://avatars.githubusercontent.com/u/809529?v=4&size=40)![claude](https://avatars.githubusercontent.com/u/81847?v=4&size=40)

[ajayr](https://github.com/bytedance/deer-flow/commits?author=ajayr)

and

[claude](https://github.com/bytedance/deer-flow/commits?author=claude)

[feat(channels): add Buzz (Nostr) channel connector (](https://github.com/bytedance/deer-flow/commit/d732b90dc3737091dedf842e42eac02ba5230c40) [#4649](https://github.com/bytedance/deer-flow/pull/4649) [)](https://github.com/bytedance/deer-flow/commit/d732b90dc3737091dedf842e42eac02ba5230c40)

Open commit detailssuccess

Aug 5, 2026

[d732b90](https://github.com/bytedance/deer-flow/commit/d732b90dc3737091dedf842e42eac02ba5230c40) · Aug 5, 2026

## History

[History](https://github.com/bytedance/deer-flow/commits/main/backend/pyproject.toml)

Open commit details

History

89 lines (83 loc) · 3.49 KB

## FilesExpand file tree

main

/

# pyproject.toml

Copy path

Top

## File metadata and controls

- Code

- Blame

89 lines (83 loc) · 3.49 KB

[Raw](https://github.com/bytedance/deer-flow/raw/refs/heads/main/backend/pyproject.toml)

Copy raw file

Download raw file

Open symbols panel

Edit and raw actions

\[project\] name = "deer-flow" version = "2.1.0" description = "LangGraph-based AI agent system with sandbox execution capabilities" readme = "README.md" requires-python = ">=3.12" dependencies = \[ "deerflow-harness", "fastapi>=0.115.0", "httpx>=0.28.0", "python-multipart>=0.0.31", "sse-starlette>=2.1.0", "uvicorn\[standard\]>=0.34.0", "lark-oapi>=1.4.0", "slack-sdk>=3.33.0", "python-telegram-bot>=21.0", "langgraph-sdk>=0.1.51", "markdown-to-mrkdwn>=0.3.1", "wecom-aibot-python-sdk>=0.1.6", "dingtalk-stream>=0.24.3", "bcrypt>=4.0.0", "pyjwt>=2.13.0", "email-validator>=2.0.0", "e2b-code-interpreter>=2.8.1", \] \[project.optional-dependencies\] postgres = \["deerflow-harness\[postgres\]"\] redis = \["deerflow-harness\[redis\]"\] discord = \["discord.py>=2.7.0"\] buzz = \["coincurve>=20.0.0"\] monocle = \["deerflow-harness\[monocle\]"\] browser = \["deerflow-harness\[browser\]"\] memory-zh = \["deerflow-harness\[memory-zh\]"\] \[dependency-groups\] dev = \[ "blockbuster>=1.5.26,<1.6", "hypothesis>=6.100,<7", "jsonschema>=4.26.0", "prompt-toolkit>=3.0.0", "pytest>=9.0.3", "pytest-asyncio>=1.3.0", "ruff>=0.14.11", # Monocle tracer (also the deerflow-harness\[monocle\] extra); kept in the dev # group so the tracing tests can import it without forcing it onto installs. "monocle\_apptrace>=0.8.8", # redis is an optional runtime extra (deerflow-harness\[redis\]); pin it in the # dev group so the stream-bridge tests can always import/exercise the redis # bridge without forcing it onto production installs. "redis>=5.0.0", # TUI runtime dep (also declared as the deerflow-harness\[tui\] extra); kept in # the dev group so the terminal workbench can be run and tested locally / in CI. "textual>=0.80", \] \[tool.pytest.ini\_options\] markers = \[ "no\_auto\_user: disable the conftest autouse contextvar fixture for this test", "allow\_blocking\_io: opt out of the strict Blockbuster gate in tests/blocking\_io/", "integration: tests that require an external service (e.g. Redis); skipped when unavailable", "live: tests that call real external APIs and require explicit opt-in", \] \[tool.uv\] index-url = "https://pypi.org/simple" # langgraph-sdk 0.4.2 (pulled in by langgraph 1.2.9 for DeltaChannel) pins # \`websockets<16,>=14\`, silently downgrading websockets 16.0 -> 15.0.1. The # pin is not grounded in any API incompatibility: websockets 16's only # breaking change is requiring Python >=3.10 (we require >=3.12), the sdk # only imports \`websockets.asyncio.client\`/\`websockets.exceptions\` (both # 16-compatible), and DeerFlow never uses the sdk's WebSocket transport # (httpx/SSE only). DeerFlow does have one direct consumer of its own: the Buzz # channel (\`app/channels/buzz.py\`) imports the top-level \`websockets\` package and # calls \`websockets.connect()\`, which in 16.0 is the same asyncio client the sdk # uses, re-exported at the package root -- so it is covered by the same # compatibility argument. Pin the exact pre-upgrade 16.0 for that plus the IM # channel integrations (dingtalk-stream, python-telegram-bot, etc.) that ran on # it before. Remove once langgraph-sdk relaxes the pin upstream. Note: enabling # the \`openai\[realtime\]\` or \`slack-sdk\[optional\]\` extras would conflict (they # also cap websockets<16). override-dependencies = \["websockets==16.0"\] \[tool.uv.workspace\] members = \["packages/harness", "packages/extension-api"\] \[tool.uv.sources\] deerflow-harness = { workspace = true } deerflow-extension-api = { workspace = true }

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

48

49

50

51

52

53

54

55

56

57

58

59

60

61

62

63

64

65

66

67

68

69

70

71

72

73

74

75

76

77

78

79

80

81

82

83

84

85

86

87

88

89

\[project\]

name = "deer-flow"

version = "2.1.0"

description = "LangGraph-based AI agent system with sandbox execution capabilities"

readme = "README.md"

requires-python = "\>=3.12"

dependencies = \[

"deerflow-harness",

"fastapi>=0.115.0",

"httpx>=0.28.0",

"python-multipart>=0.0.31",

"sse-starlette>=2.1.0",

"uvicorn\[standard\]>=0.34.0",

"lark-oapi>=1.4.0",

"slack-sdk>=3.33.0",

"python-telegram-bot>=21.0",

"langgraph-sdk>=0.1.51",

"markdown-to-mrkdwn>=0.3.1",

"wecom-aibot-python-sdk>=0.1.6",

"dingtalk-stream>=0.24.3",

"bcrypt>=4.0.0",

"pyjwt>=2.13.0",

"email-validator>=2.0.0",

"e2b-code-interpreter>=2.8.1",

\]

\[project.optional-dependencies\]

postgres = \["deerflow-harness\[postgres\]"\]

redis = \["deerflow-harness\[redis\]"\]

discord = \["discord.py>=2.7.0"\]

buzz = \["coincurve>=20.0.0"\]

monocle = \["deerflow-harness\[monocle\]"\]

browser = \["deerflow-harness\[browser\]"\]

memory-zh = \["deerflow-harness\[memory-zh\]"\]

\[dependency-groups\]

dev = \[

"blockbuster>=1.5.26,<1.6",

"hypothesis>=6.100,<7",

"jsonschema>=4.26.0",

"prompt-toolkit>=3.0.0",

"pytest>=9.0.3",

"pytest-asyncio>=1.3.0",

"ruff>=0.14.11",

# Monocle tracer (also the deerflow-harness\[monocle\] extra); kept in the dev

# group so the tracing tests can import it without forcing it onto installs.

"monocle\_apptrace>=0.8.8",

# redis is an optional runtime extra (deerflow-harness\[redis\]); pin it in the

# dev group so the stream-bridge tests can always import/exercise the redis

# bridge without forcing it onto production installs.

"redis>=5.0.0",

# TUI runtime dep (also declared as the deerflow-harness\[tui\] extra); kept in

# the dev group so the terminal workbench can be run and tested locally / in CI.

"textual>=0.80",

\]

\[tool.pytest.ini\_options\]

markers = \[

"no\_auto\_user: disable the conftest autouse contextvar fixture for this test",

"allow\_blocking\_io: opt out of the strict Blockbuster gate in tests/blocking\_io/",

"integration: tests that require an external service (e.g. Redis); skipped when unavailable",

"live: tests that call real external APIs and require explicit opt-in",

\]

\[tool.uv\]

index-url = "https://pypi.org/simple"

# langgraph-sdk 0.4.2 (pulled in by langgraph 1.2.9 for DeltaChannel) pins

# \`websockets<16,>=14\`, silently downgrading websockets 16.0 -> 15.0.1. The

# pin is not grounded in any API incompatibility: websockets 16's only

# breaking change is requiring Python >=3.10 (we require >=3.12), the sdk

# only imports \`websockets.asyncio.client\`/\`websockets.exceptions\` (both

# 16-compatible), and DeerFlow never uses the sdk's WebSocket transport

# (httpx/SSE only). DeerFlow does have one direct consumer of its own: the Buzz

# channel (\`app/channels/buzz.py\`) imports the top-level \`websockets\` package and

# calls \`websockets.connect()\`, which in 16.0 is the same asyncio client the sdk

# uses, re-exported at the package root -- so it is covered by the same

# compatibility argument. Pin the exact pre-upgrade 16.0 for that plus the IM

# channel integrations (dingtalk-stream, python-telegram-bot, etc.) that ran on

# it before. Remove once langgraph-sdk relaxes the pin upstream. Note: enabling

# the \`openai\[realtime\]\` or \`slack-sdk\[optional\]\` extras would conflict (they

# also cap websockets<16).

override-dependencies = \["websockets==16.0"\]

\[tool.uv.workspace\]

members = \["packages/harness", "packages/extension-api"\]

\[tool.uv.sources\]

deerflow-harness = { workspace = true }

deerflow-extension-api = { workspace = true }