<div align="center">

# Two threads of semver for more flexibility
## THREAD => KLYNTAR

</div>

<br><br>

### <b>Abstract</b>

Version tracking is very important to keep backward compatibility and bring new features. Due to architecture of Klyntar and symbiotes based on it,we propose to track 2 threads of versioning.

## Threads for the first time

|     Thread ID     |                   General description                        |
|:------------------|:-------------------------------------------------------------|
| <b>CORE_VERSION</b>      | Common versions flow for all the symbiotes for compatibility |
| <b>SYMBIOTE_VERSION</b>  | Symbiote own flow with private features & functions          |