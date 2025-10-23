## To strat a new tmux session
```
tmux
```

## To create a pane, split vertically
```
ctrl a + shift 5
```

## To switch between panes.
```
ctrl a + (arrow keys) 
```

## To create a pane, split horizontally
```
ctrl a + shift '
```

To close the panes
```
exit
```

## To create a new window
```
ctrl a + c
```

## To switch between windows
```
ctrl a + 0
```

## To Rename window
```
ctrl a + ,
```

## session
## To detach from a session
ctrl a + d

## to view session from background
```
tmux ls
```
summary gives how many windows you opened in a session & when it was created


## To attach to session
```
tmux attach -t 0
```

## To rename a session
```
tmux rename-session -t 0 git
```

## To create a new session with name
```
tmux new -s docker
```

## killing session
```
tmux kill-session -t docker
```

## nested tmux session

To create window on the second level
```
ctrl g + c
```

