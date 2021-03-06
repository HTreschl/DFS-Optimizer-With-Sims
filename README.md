# DFS Optimizer

A library designed to run sims and optimize lineups for DFS using python's pulp module. Includes NFL and MLB.

# NFL Example -- Single Optimized Lineup for a Classic Game-Type
Optimize a single lineup without running any sims using the example projections for a classic dfs game

Import the data and initialize the NFL optimizer

```
df = pd.read_excel('NFL DK Projections.xlsx')
model = opt.NFL(df=df)
```

Optimize using the projection set we want, in this case averages of all available projections

```
lineup = model.standard_optimizer(df, objective_fn_column='avg fpts')
print(lineup)
```

Returns a list of players in the lineup, in this case 

['Curtis Samuel', 'Davante Adams', 'David Montgomery', 'Deebo Samuel', 'Derrick Henry', 'Josh Allen', 'Lions', 'Mike Davis', 'Will Dissly']

# Running Sims

the runSims module adds functionality simulate results from each player and provide an optimal ownership calculation. Players' point predictions are sampled from a normal distribution centered on their fantasy point projection and with a 95% CI from 0 to 2x their projected points. Returns optimal ownership and leverage, where optimal ownership is the percentage of simulations in which the player was in the optimal lineup, and leverage is the difference between optimal ownership and projected ownership.
