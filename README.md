# CHANGELOG

Golang deps proj manager, like rebar in Erlang. Clone all deps project in `vendor` directory when you run `gopack get-deps`.
Fork from https://github.com/d2fn/gopack, change the vendor directory struct.

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





------------------------------------

# gopack

![](https://travis-ci.org/d2fn/gopack.png)

The [natural logarithm](https://en.wikipedia.org/wiki/Natural_logarithm) to Go's [e](http://en.wikipedia.org/wiki/E_%28mathematical_constant%29). Simple package management for Go a la [rebar](https://github.com/basho/rebar).

A configuration file named `gopack.config` tells gopack about your dependencies and which version should be included. You can point to a tag, a branch, or, if you are being naughty, master. The programming community would thank you not to carry out such a travesty as it leaves your code open to breaking changes. Much better to point at _immutable_ code.

##### gopack.config

```toml
[deps.memcache]
import = "github.com/bradfitz/gomemcache/memcache"
tag = "1.2"

[deps.mux]
import = "github.com/gorilla/mux"
branch = "1.0rc2"

[deps.toml]
import = "github.com/pelletier/go-toml"
commit = "23d36c08ab90f4957ae8e7d781907c368f5454dd"
```
Inside the configuration file you can also specify your project's repository name and it will be linked before pulling dependencies.
For instance, let's say you have a reference to a subdirectory from your own project like this:

```go
import "github.com/login/repo/dir"
```

You can declare it's repository name and it won't be pulled from the remote repo:

```toml
repo = "github.com/login/repo"

# Put other dependencies here.
```

Then simply run, install, and test your code much as you would have with the ```go``` command. Just replace ```go``` with ```gp```.

```gp test```
```gp run *.go```

etc…

The ```gp``` command will make sure your dependencies are downloaded, their respective git repos are pointed at the appropriate tag or branch, and your code is compiled against the desired library versions. Project dependencies are stored locally in the ```vendor``` directory.

## Installation

First checkout and build from source
```
git clone git@github.com:d2fn/gopack.git
cd gopack
go get github.com/pelletier/go-toml && go build -o gp
```

Then copy the ```gopack``` binary to your project directory and invoke just as you would ```go```. Make sure the current directory is on your path or place the ```gp``` binary elsewhere on your path.
```
cp gp ~/projects/mygoproject
cd ~/projects/myproject
gp run *.go
```

## Sources and Scms

Gopack uses `goget` to download packages by default, but when you need more control over downloads you can be more specific about the source and the type of scm.

For example, if you want to download the source using git via ssh, you can provide the ssh url and specify `git` as a scm:

```toml
[deps.mux]
import = "github.com/gorilla/mux"
source = "git@github.com:gorilla/mux.git"
scm = "git"
```

You can do the same with Mercurial, `hg`, and Subversion, `svn`.

## Gopack commands

Gopack includes a few tools to help you track your project dependencies.

1. `./gp dependencytree` shows the complete list of external dependencies in your project.
2. `./gp stats` shows statistics about dependency imports.
3. `./gp installdeps` installs the project dependencies using `go install ...`.

## License

Copyright (c) 2013 Dietrich Featherston

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
