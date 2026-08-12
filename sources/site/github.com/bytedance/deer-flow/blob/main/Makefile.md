# Source: https://github.com/bytedance/deer-flow/blob/main/Makefile

### Uh oh!

There was an error while loading. [Please reload this page]().

[bytedance](https://github.com/bytedance) / **[deer-flow](https://github.com/bytedance/deer-flow)** Public

- [Notifications](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow) You must be signed in to change notification settings
- [Fork 10.9k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)
- [Star 79.8k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)

 ## FilesExpand file tree

main

/

# Makefile

Copy path

Blame

More file actions

Blame

More file actions

## Latest commit

[![heart-scalpel](https://avatars.githubusercontent.com/u/61306204?v=4&size=40)](https://github.com/heart-scalpel) [heart-scalpel](https://github.com/bytedance/deer-flow/commits?author=heart-scalpel)

[feat: complete backend thread-boundary inventory (](https://github.com/bytedance/deer-flow/commit/d3ce5de218853e7cca6136a9ed9ba63111787158) [#4562](https://github.com/bytedance/deer-flow/pull/4562) [)](https://github.com/bytedance/deer-flow/commit/d3ce5de218853e7cca6136a9ed9ba63111787158)

Open commit detailsfailure

Jul 29, 2026

[d3ce5de](https://github.com/bytedance/deer-flow/commit/d3ce5de218853e7cca6136a9ed9ba63111787158) · Jul 29, 2026

## History

[History](https://github.com/bytedance/deer-flow/commits/main/Makefile)

Open commit details

History

176 lines (145 loc) · 6.31 KB

## FilesExpand file tree

main

/

# Makefile

Copy path

Top

## File metadata and controls

- Code

- Blame

176 lines (145 loc) · 6.31 KB

[Raw](https://github.com/bytedance/deer-flow/raw/refs/heads/main/Makefile)

Copy raw file

Download raw file

Open symbols panel

Edit and raw actions

\# DeerFlow - Unified Development Environment .PHONY: help config config-upgrade check install setup doctor support-bundle detect-thread-boundaries detect-blocking-io dev dev-daemon start start-daemon nginx stop up down clean docker-init docker-start docker-stop docker-logs docker-logs-frontend docker-logs-gateway docker-logs-redis BASH ?= bash BACKEND\_UV\_RUN = cd backend && uv run # Detect OS for Windows compatibility ifeq ($(OS),Windows\_NT) SHELL := cmd.exe PYTHON ?= python # Run repo shell scripts through Git Bash when Make is launched from cmd.exe / PowerShell. RUN\_WITH\_GIT\_BASH = call scripts\\run-with-git-bash.cmd else PYTHON ?= python3 RUN\_WITH\_GIT\_BASH = endif FRONTEND\_PNPM = $(PYTHON) ../scripts/pnpm.py help: @echo "DeerFlow Development Commands:" @echo " make setup - Interactive setup wizard (recommended for new users)" @echo " make doctor - Check configuration and system requirements" @echo " make support-bundle - Create a redacted issue summary, AI draft, and evidence bundle" @echo " make config - Generate local config files (aborts if config already exists)" @echo " make config-upgrade - Merge new fields from config.example.yaml into config.yaml" @echo " make check - Check if all required tools are installed" @echo " make detect-thread-boundaries - Inventory backend executor/thread/event-loop boundaries" @echo " make detect-blocking-io - Inventory blocking IO that may block the backend event loop" @echo " make install - Install all dependencies (frontend + backend + pre-commit hooks)" @echo " make setup-sandbox - Pre-pull sandbox container image (recommended)" @echo " make dev - Start all services in development mode (with hot-reloading)" @echo " make dev-daemon - Start dev services in background (daemon mode)" @echo " make start - Start all services in production mode (optimized, no hot-reloading)" @echo " make start-daemon - Start prod services in background (daemon mode)" @echo " make nginx - Start nginx alone in the foreground (local dev config)" @echo " make stop - Stop all running services" @echo " make clean - Clean up processes and temporary files" @echo "" @echo "Docker Production Commands:" @echo " make up - Build and start production Docker services (localhost:2026)" @echo " make down - Stop and remove production Docker containers" @echo "" @echo "Docker Development Commands:" @echo " make docker-init - Pull the sandbox image" @echo " make docker-start - Start Docker services (mode-aware from config.yaml, localhost:2026)" @echo " make docker-stop - Stop Docker development services" @echo " make docker-logs - View Docker development logs" @echo " make docker-logs-frontend - View Docker frontend logs" @echo " make docker-logs-gateway - View Docker gateway logs" @echo " make docker-logs-redis - View Docker Redis logs" ## Setup & Diagnosis setup: @$(BACKEND\_UV\_RUN) python ../scripts/setup\_wizard.py doctor: @$(BACKEND\_UV\_RUN) python ../scripts/doctor.py support-bundle: @$(BACKEND\_UV\_RUN) python ../scripts/support\_bundle.py --include-doctor detect-thread-boundaries: @$(BACKEND\_UV\_RUN) python ../scripts/detect\_thread\_boundaries.py --json-output ../.deer-flow/thread-boundary-inventory.json detect-blocking-io: @$(MAKE) -C backend detect-blocking-io config: @$(PYTHON) ./scripts/configure.py config-upgrade: @$(RUN\_WITH\_GIT\_BASH) ./scripts/config-upgrade.sh # Check required tools check: @$(PYTHON) ./scripts/check.py # Install all dependencies install: @echo "Installing backend dependencies..." @cd backend && uv sync @echo "Installing frontend dependencies..." @cd frontend && $(FRONTEND\_PNPM) install @echo "Installing pre-commit hooks..." @uv tool install pre-commit @pre-commit install --overwrite @echo "✓ All dependencies installed" @echo "" @echo "==========================================" @echo " Optional: Pre-pull Sandbox Image" @echo "==========================================" @echo "" @echo "If you plan to use Docker/Container-based sandbox, you can pre-pull the image:" @echo " make setup-sandbox" @echo "" # Pre-pull sandbox Docker image (optional but recommended) setup-sandbox: @$(RUN\_WITH\_GIT\_BASH) ./scripts/setup-sandbox.sh # Start all services in development mode (with hot-reloading) dev: @$(PYTHON) ./scripts/check.py @$(RUN\_WITH\_GIT\_BASH) ./scripts/serve.sh --dev # Start all services in production mode (with optimizations) start: @$(PYTHON) ./scripts/check.py @$(RUN\_WITH\_GIT\_BASH) ./scripts/serve.sh --prod # Start all services in daemon mode (background) dev-daemon: @$(PYTHON) ./scripts/check.py @$(RUN\_WITH\_GIT\_BASH) ./scripts/serve.sh --dev --daemon # Start prod services in daemon mode (background) start-daemon: @$(PYTHON) ./scripts/check.py @$(RUN\_WITH\_GIT\_BASH) ./scripts/serve.sh --prod --daemon # Start nginx alone in the foreground with the local dev config nginx: @$(RUN\_WITH\_GIT\_BASH) ./scripts/nginx.sh # Stop all services stop: @$(RUN\_WITH\_GIT\_BASH) ./scripts/serve.sh --stop # Clean up clean: stop @echo "Cleaning up..." @-rm -rf backend/.deer-flow 2>/dev/null || true @-rm -rf logs/\*.log 2>/dev/null || true @echo "✓ Cleanup complete" # ========================================== # Docker Development Commands # ========================================== # Initialize Docker containers and install dependencies docker-init: @$(RUN\_WITH\_GIT\_BASH) ./scripts/docker.sh init # Start Docker development environment docker-start: @$(RUN\_WITH\_GIT\_BASH) ./scripts/docker.sh start # Stop Docker development environment docker-stop: @$(RUN\_WITH\_GIT\_BASH) ./scripts/docker.sh stop # View Docker development logs docker-logs: @$(RUN\_WITH\_GIT\_BASH) ./scripts/docker.sh logs # View Docker development logs docker-logs-frontend: @$(RUN\_WITH\_GIT\_BASH) ./scripts/docker.sh logs --frontend docker-logs-gateway: @$(RUN\_WITH\_GIT\_BASH) ./scripts/docker.sh logs --gateway docker-logs-redis: @$(RUN\_WITH\_GIT\_BASH) ./scripts/docker.sh logs --redis # ========================================== # Production Docker Commands # ========================================== # Build and start production services up: @$(RUN\_WITH\_GIT\_BASH) ./scripts/deploy.sh # Stop and remove production containers down: @$(RUN\_WITH\_GIT\_BASH) ./scripts/deploy.sh down

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

90

91

92

93

94

95

96

97

98

99

100

101

102

103

104

105

106

107

108

109

110

111

112

113

114

115

116

117

118

119

120

121

122

123

124

125

126

127

128

129

130

131

132

133

134

135

136

137

138

139

140

141

142

143

144

145

146

147

148

149

150

151

152

153

154

155

156

157

158

159

160

161

162

163

164

165

166

167

168

169

170

171

172

173

174

175

176

# DeerFlow - Unified Development Environment

.PHONY: help config config-upgrade check install setup doctor support-bundle detect-thread-boundaries detect-blocking-io dev dev-daemon start start-daemon nginx stop up down clean docker-init docker-start docker-stop docker-logs docker-logs-frontend docker-logs-gateway docker-logs-redis

BASH ?= bash

BACKEND\_UV\_RUN = cd backend && uv run

# Detect OS for Windows compatibility

ifeq ($(OS),Windows\_NT)

SHELL := cmd.exe

PYTHON ?= python

# Run repo shell scripts through Git Bash when Make is launched from cmd.exe / PowerShell.

RUN\_WITH\_GIT\_BASH = call scripts\\run-with-git-bash.cmd

else

PYTHON ?= python3

RUN\_WITH\_GIT\_BASH =

endif

FRONTEND\_PNPM = $(PYTHON) ../scripts/pnpm.py

help:

@echo "DeerFlow Development Commands:"

@echo " make setup - Interactive setup wizard (recommended for new users)"

@echo " make doctor - Check configuration and system requirements"

@echo " make support-bundle - Create a redacted issue summary, AI draft, and evidence bundle"

@echo " make config - Generate local config files (aborts if config already exists)"

@echo " make config-upgrade - Merge new fields from config.example.yaml into config.yaml"

@echo " make check - Check if all required tools are installed"

@echo " make detect-thread-boundaries - Inventory backend executor/thread/event-loop boundaries"

@echo " make detect-blocking-io - Inventory blocking IO that may block the backend event loop"

@echo " make install - Install all dependencies (frontend + backend + pre-commit hooks)"

@echo " make setup-sandbox - Pre-pull sandbox container image (recommended)"

@echo " make dev - Start all services in development mode (with hot-reloading)"

@echo " make dev-daemon - Start dev services in background (daemon mode)"

@echo " make start - Start all services in production mode (optimized, no hot-reloading)"

@echo " make start-daemon - Start prod services in background (daemon mode)"

@echo " make nginx - Start nginx alone in the foreground (local dev config)"

@echo " make stop - Stop all running services"

@echo " make clean - Clean up processes and temporary files"

@echo ""

@echo "Docker Production Commands:"

@echo " make up - Build and start production Docker services (localhost:2026)"

@echo " make down - Stop and remove production Docker containers"

@echo ""

@echo "Docker Development Commands:"

@echo " make docker-init - Pull the sandbox image"

@echo " make docker-start - Start Docker services (mode-aware from config.yaml, localhost:2026)"

@echo " make docker-stop - Stop Docker development services"

@echo " make docker-logs - View Docker development logs"

@echo " make docker-logs-frontend - View Docker frontend logs"

@echo " make docker-logs-gateway - View Docker gateway logs"

@echo " make docker-logs-redis - View Docker Redis logs"

#\# Setup & Diagnosis

setup:

@$(BACKEND\_UV\_RUN) python ../scripts/setup\_wizard.py

doctor:

@$(BACKEND\_UV\_RUN) python ../scripts/doctor.py

support-bundle:

@$(BACKEND\_UV\_RUN) python ../scripts/support\_bundle.py --include-doctor

detect-thread-boundaries:

@$(BACKEND\_UV\_RUN) python ../scripts/detect\_thread\_boundaries.py --json-output ../.deer-flow/thread-boundary-inventory.json

detect-blocking-io:

@$(MAKE) -C backend detect-blocking-io

config:

@$(PYTHON) ./scripts/configure.py

config-upgrade:

@$(RUN\_WITH\_GIT\_BASH) ./scripts/config-upgrade.sh

# Check required tools

check:

@$(PYTHON) ./scripts/check.py

# Install all dependencies

install:

@echo "Installing backend dependencies..."

@cd backend && uv sync

@echo "Installing frontend dependencies..."

@cd frontend && $(FRONTEND\_PNPM) install

@echo "Installing pre-commit hooks..."

@uv tool install pre-commit

@pre-commit install --overwrite

@echo "✓ All dependencies installed"

@echo ""

@echo "\=========================================="

@echo " Optional: Pre-pull Sandbox Image"

@echo "\=========================================="

@echo ""

@echo "If you plan to use Docker/Container-based sandbox, you can pre-pull the image:"

@echo " make setup-sandbox"

@echo ""

# Pre-pull sandbox Docker image (optional but recommended)

setup-sandbox:

@$(RUN\_WITH\_GIT\_BASH) ./scripts/setup-sandbox.sh

# Start all services in development mode (with hot-reloading)

dev:

@$(PYTHON) ./scripts/check.py

@$(RUN\_WITH\_GIT\_BASH) ./scripts/serve.sh --dev

# Start all services in production mode (with optimizations)

start:

@$(PYTHON) ./scripts/check.py

@$(RUN\_WITH\_GIT\_BASH) ./scripts/serve.sh --prod

# Start all services in daemon mode (background)

dev-daemon:

@$(PYTHON) ./scripts/check.py

@$(RUN\_WITH\_GIT\_BASH) ./scripts/serve.sh --dev --daemon

# Start prod services in daemon mode (background)

start-daemon:

@$(PYTHON) ./scripts/check.py

@$(RUN\_WITH\_GIT\_BASH) ./scripts/serve.sh --prod --daemon

# Start nginx alone in the foreground with the local dev config

nginx:

@$(RUN\_WITH\_GIT\_BASH) ./scripts/nginx.sh

# Stop all services

stop:

@$(RUN\_WITH\_GIT\_BASH) ./scripts/serve.sh --stop

# Clean up

clean: stop

@echo "Cleaning up..."

@-rm -rf backend/.deer-flow 2>/dev/null || true

@-rm -rf logs/\*.log 2>/dev/null || true

@echo "✓ Cleanup complete"

# ==========================================

# Docker Development Commands

# ==========================================

# Initialize Docker containers and install dependencies

docker-init:

@$(RUN\_WITH\_GIT\_BASH) ./scripts/docker.sh init

# Start Docker development environment

docker-start:

@$(RUN\_WITH\_GIT\_BASH) ./scripts/docker.sh start

# Stop Docker development environment

docker-stop:

@$(RUN\_WITH\_GIT\_BASH) ./scripts/docker.sh stop

# View Docker development logs

docker-logs:

@$(RUN\_WITH\_GIT\_BASH) ./scripts/docker.sh logs

# View Docker development logs

docker-logs-frontend:

@$(RUN\_WITH\_GIT\_BASH) ./scripts/docker.sh logs --frontend

docker-logs-gateway:

@$(RUN\_WITH\_GIT\_BASH) ./scripts/docker.sh logs --gateway

docker-logs-redis:

@$(RUN\_WITH\_GIT\_BASH) ./scripts/docker.sh logs --redis

# ==========================================

# Production Docker Commands

# ==========================================

# Build and start production services

up:

@$(RUN\_WITH\_GIT\_BASH) ./scripts/deploy.sh

# Stop and remove production containers

down:

@$(RUN\_WITH\_GIT\_BASH) ./scripts/deploy.sh down