# Tic Tac Toe


## Methods

### Join()

```txt
state := getProvisionalState()

if state.playerTwoJoined
	return Error('Player two has already joined')

return Action(JOIN)
```

### Claim(player, idx)

```txt
state := getProvisionalState()

if gameOver(state.board)
	return Error('The game is lost, you need to forfeit')

if state.move %2 is not player
	return Error('It is not your turn')

if state.board[idx] is not -1
	return Error('That cell is already marked')

return Action(CLAIM, player, idx)
```

### Forfeit(player)

```txt
state := getProvisionalState()

if state.move %2 is not player
	return Error('It is not your turn')

return Action(FORFEIT, player)
```

### Tie(player)

```txt
state := getProvisionalState()

if state.move %2 is not player
	return Error('It is not your turn')

if gameOver(state.board)
	return Error('The game is lost, you need to forfeit')

if isNotFilled(state.board)
	return Error('Cannot tie until the board is filled')

return Action(TIE, player)
```

## Actions

### Action(JOIN)

* *(no parameters)*

### Action(CLAIM, player, idx)

* player *Enum* - Either `0` or `1`
* idx *Integer* - An integer in the range `(0, 8)`

### Action(FORFEIT, player)

* player *Enum* - Either `0` or `1`

### Action(TIE, player)

* player *Enum* - Either `0` or `1`

## Reducer

```txt
if state is null
	state := Dictionary()

	// The board is a 3x3 grid of cells laid out like this:
	// 0 1 2
	// 3 4 5
	// 6 7 8

	state.board := Array([-1, -1, -1, -1, -1, -1, -1, -1, -1])
	state.move := 0
	state.game := 0
	state.playerTwoJoined := false
	state.gameLosers := new Array()
else
	state := state.copy()

if action.type is JOIN
	state.playerTwoJoined := true

if action.type is CLAIM
	state.board[action.idx] = action.player
	state.move := state.move + 1

if action.type = FORFEIT
	state.board := Array([-1, -1, -1, -1, -1, -1, -1, -1, -1])
	state.move := 0
	state.game := state.game + 1
	state.gameLosers.push(action.player)

if action.type = TIE
	state.board := Array([-1, -1, -1, -1, -1, -1, -1, -1, -1])
	state.move := 0
	state.game := state.game + 1
	state.gameLosers.push(-1)

return state
```

[Live Demo](https://conflux-demos.herokuapp.com/tic-tac-toe)

[Source Code](https://github.com/ben-ng/conflux-demos/tree/master/demos/tic-tac-toe)

