# Galapagos-Politics-Simulator
A concurrent cellular automaton, modelling interactions between finches in the Galapagos Islands, based on their social or political strategies. Each finch represents a political ideology, and interacts with its neighbors under local rules that govern cooperation, punishment and reproduction. This project was written in Haskell. 

## Overview
In this simulation, each finch lives on a 2D grid(which represents the Galapagos Islands) and has the following: 
- HP (health points): a resource determines survival and reproduction
- Strategy: determines how it responds to neighbors
- Interactions: occurs in local 2x2 Margolus blocks with timed message-passing concurrency
- Rules: defines the rules that allow the finches to meet, groom and ignore other finches

Each simulation step involves the following: 
1. Each cell interacting with its neighbors. 
2. Updating health and memory.
3. Shifting Margolus tiling to ensure coverage of all neighbors over time.

### Political Strategy 
- Communism: Always grooms the other finch.
- Capitalist: Grooms only when profitable.
- Authoritarian: Punishes defection permanently.
- Isolationist: Interacts only with known allies.
- Populist: Mirrors local majority behavior.
- Coalition:

## Architecture 
- BlockAutomaton.Server: Concurrent Simulation engine handling message passing, timeouts and synchronization across the grid
- BlockAutomaton.Rules: Defines Margolus positions, interactions, and cell lifecycle rules.
- Galapagos.Rules: Strategy logic: how the finches meet, groom, age, reproduce.
- Galapagos.Parser: Custom DSL parser for .rules config files.
- APL.Parser: Expression parser for embedded mini-language controlling conditional logic inside strategies.
- viewer.hs: Visualization and renders simulation in the terminal/GUI.

## Building and Running
### Requirements 
- GHC 9.8+
- Cabal 3.0+
- Linux, macOS

### Build 
```
cabal build
```
### Run Simulation 
```
cabal run viewer example.rules
```
### Run Tests 
```
cabal run exam-test
```
### Clean 
```
cabal clean
```

## Technical Highlights 
- This project has a fully concurrent cell process with message passing.
- Timeout-based safety to kill infinite loops or illegal strategies
- Uses Margolus tiling for reversible, physically-inspired simulation.
- Custom APL-like DSL parser for strategy definition.
- Property based tests for parser correctness and parameters ordering.
- Highly modular: strategies and rules can be swapped dynamically.
