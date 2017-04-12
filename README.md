# Gopack

Golang deps proj manager, like rebar in Erlang. Clone all deps project in `vendor` directory when you run `gopack get-deps`.
Fork from https://github.com/d2fn/gopack, and make some changes.

# How to use

1. go get github.com/songcf/gopack && go build -o gopack
2. copy gopack to your project
3. touch `gopack.config` file in your project, and config deps proj (you can config git/svn/hg, tag/branch/commit):
```
[deps.logrus]
import = "github.com/Sirupsen/logrus"
source = "https://github.com/Sirupsen/logrus"
scm = "git"
tag = "v0.11.5"

[deps.proto]
import = "github.com/golang/protobuf"
source = "https://github.com/golang/protobuf"
scm = "git"
branch = "master"

[deps.mysql]
import = "github.com/go-sql-driver/mysql"
source = "https://github.com/go-sql-driver/mysql"
scm = "git"
tag = "v1.3"
```

4. run `./gopack get-deps`, will create vendor dir, and git clone these deps proj

# Command
Gopack includes a few tools to help you track your project dependencies.

1. `./gopack tree` shows the complete list of external dependencies in your project.
2. `./gopack stats` shows statistics about dependency imports.
3. `./gopack get-deps` clone the project dependencies in vendor direcotry.
