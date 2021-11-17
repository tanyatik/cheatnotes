### Handy helper to create help for Makefile files

If the targest are writtn in a way:

```
target: ## help text
     stuff
```

Then the following snippet will create a handy help text:

```
$ make help
help            show this help
target          help text
```

```
help: ## show this help
    @grep -E '^[a-zA-Z_-]+:.*?## .*$$' $(MAKEFILE_LIST) \
        | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%s\033[0m|%s\n", $$1, $$2}' \
        | column -t -s '|'
```
