# Go Contribution Guidelines

Many IPFS projects use Go. Please check these guidelines before contributing go code to an IPFS repository.

## Requirements

- Run `go fmt` before pushing any code.
- Run `golint` and `go vet` too -- some things (like protobuf files) are expected to fail.

## A Short Introduction

If you are new to our Go development workflow:

- Ensure you have [Go installed on your system](https://golang.org/doc/install).
- Make sure that you have the environment variable `GOPATH` set somewhere, e.g. `$HOME/gopkg`
- Clone ipfs into the path `$GOPATH/src/github.com/ipfs/go-ipfs`
  - NOTE: This is true even if you have forked go-ipfs, dependencies in go are path based and must be in the right locations.
- You are now free to make changes to the codebase as you please.
- You can build the binary by running `go build ./cmd/ipfs` from the go-ipfs directory.
  - NOTE: when making changes remember to restart your daemon to ensure its running your new code.
  
## Imports

We strive to use the following convention when it comes to imports. First list stdlib imports, then local repository imports and then all other external imports. Separate them using one empty new line so they are not reordered by `go fmt` or `goimports`.

Example:
```go
import (
	"context"
	"errors"
	"sync"
	"sync/atomic"

	blocks "github.com/ipfs/go-ipfs/blocks"
	dshelp "github.com/ipfs/go-ipfs/thirdparty/ds-help"

	logging "gx/ipfs/QmSpJByNKFX1sCsHBEp3R73FL4NF6FnQTEGyNAXHm2GS52/go-log"
	ds "gx/ipfs/QmbzuUusHqaLLoNTDEVLcSF6vZDHZDLPC7p4bztRvvkXxU/go-datastore"
	dsns "gx/ipfs/QmbzuUusHqaLLoNTDEVLcSF6vZDHZDLPC7p4bztRvvkXxU/go-datastore/namespace"
	dsq "gx/ipfs/QmbzuUusHqaLLoNTDEVLcSF6vZDHZDLPC7p4bztRvvkXxU/go-datastore/query"
	cid "gx/ipfs/QmcEcrBAMrwMyhSjXt4yfyPpzgSuV8HLHavnfmiKCSRqZU/go-cid"
)
```

If a package name isn't the same as its directory, use the explicit name.

## Pull Request Reviews

PRs and PR reviews are an important part of the our project process. As a PR contributor your goal is to help others
understand your PR as quickly and easily as possible. 
- Review your own PR before asking others. Dead code, test code, typos all will slip into PRs occasionally, and that's fine. But give it a pass first to help reviewers to focus on the actual code being submitted.
- Provide context for your PR. Provide a description of the problem your PR addresses and the solution you have provided in your initial description to help readers get started. It doesn't have to be extensive - a few sentences each.
- If there are parts of your PR you are especially unsure about, or that you know will be tricky to understand, point them out ahead of time and explain them as best as possible.

When reviewing a PR:
- All questions are good! The goal is to understand if all code is both sufficient and necessary, and first few rounds can just be adding more info to the PR via clarifications.
- Block out sufficient time for actually going as deep as possible through the code paths. 
- Consider the test coverage of the changes. Are there tests?  Do they run?
- Don't be shy. Reviewing PRs is an important part of learning the codebase. Pair-reviewing with another contributor is a helpful technique if a PR is particularly new or complex. 
