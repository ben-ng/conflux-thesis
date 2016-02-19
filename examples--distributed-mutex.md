# Distributed Mutex

## Methods

### Lock(key, nonce)

```txt
state := getProvisionalState()

if state is null OR state[key] is null
	return Action(LOCK, key, nonce)
else
	return Error('Someone else is holding on to the lock')
```

### Unlock(key, nonce)

```txt
state := getProvisionalState()

if state is not null AND state[key] is not null AND state[key] is nonce
	return Action(UNLOCK, key, nonce)
else
	return null
```

## Actions

### Action(LOCK, key, nonce, duration)

* key *String* - The dictionary key to lock
* nonce *String* - A random string, preferably a V4 UUID

### Action(UNLOCK, key, nonce)

* key *String* - The dictionary key to unlock
* nonce *String* - The same string that was used to acquire the lock

## Reducer

```txt
if state is null
	state := Dictionary()
else
	state := state.copy()

if action.type is LOCK
	state[action.key] := action.nonce

if action.type is UNLOCK
	state[action.key] := null

return state
```

[https://github.com/ben-ng/mutex-js](Source Code)
