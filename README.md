# Name conflicts when static branching with targets

{tarchetypes} does warn name conflict of names from `values` of `tar_map` and names in `command` of `tar_target`.

```r
# _targets.R
f <- \() cat("Hi")

values <- tibble::tibble(
  f = 1:10
)

list(
  tar_map(
    values = values,
    tar_target(target, f())
  )
)
```

```r
tar_make()
```

```
▶ dispatched target target_6
✖ errored target target_6
▶ completed pipeline [0.198 seconds]
Error:
! Error running targets::tar_make()
Error messages: targets::tar_meta(fields = error, complete_only = TRUE)
Debugging guide: https://books.ropensci.org/targets/debugging.html
How to ask for help: https://books.ropensci.org/targets/help.html
Last error message:
    attempt to apply non-function
Last error traceback:
    .handleSimpleError(function (condition)  {     state$error <- build_mess...
    h(simpleError(msg, call))
```

... although `tar_manifest` gives some hints.

```r
tar_manifest()
```
```
# A tibble: 10 × 2
   name      command
   <chr>     <chr>  
 1 target_6  6L()   
 2 target_10 10L()  
 3 target_7  7L()   
 4 target_8  8L()   
 5 target_9  9L()   
 6 target_1  1L()   
 7 target_2  2L()   
 8 target_3  3L()   
 9 target_4  4L()   
10 target_5  5L()   
```
