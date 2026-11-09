# Evolution of Cooperation in the Iterated Prisoner's Dilemma

A small computational study of how action errors affect cooperation in an evolving population. The project implements the memory-one strategies and genetic algorithm from Exercise 8 of the Computational Intelligence lab using Python, DEAP, and NumPy.

Completed by Miguel Ruiz and Emre Köymen.

## Research question

Does cooperation decrease as the probability of an action error increases?

Each strategy is a five-bit rule: one opening move followed by one response for each previous outcome (`CC`, `CD`, `DC`, `DD`). The bits use `0 = cooperate` and `1 = defect`, giving 32 possible strategies. The named `GRIM` rule is the memory-one strategy `00111`; it is an adaptation and cannot remember every past defection like classical Grim Trigger.

For each noise level (`0`, `0.01`, and `0.05`), a population of 100 individuals evolves for 500 generations. Each individual plays 150 rounds against every other member of its population. Fitness is the expected average payoff against the other 99 individuals.

The code calculates expected payoff matrix `A` and cooperation matrix `H` for all 32 × 32 strategy pairs. It includes action noise in the probabilities, so evolution uses exact expected match values rather than sampled match rewards. The population's initialization and genetic operators remain stochastic.

## Results

The saved study contains 30 independent runs per noise level. Median cooperation during generations 401–500 was:

| Action noise | Median cooperation |
| ---: | ---: |
| 0 | 98.0% |
| 0.01 | 47.2% |
| 0.05 | 10.0% |

The saved comparisons include bootstrap intervals, Mann–Whitney tests, Holm-adjusted p-values, and Vargha–Delaney effect sizes. The report is available at [`report/CI_Project.pdf`](report/CI_Project.pdf).

## Setup

Use Python 3.12. From this folder, create and activate a virtual environment, then install the pinned dependencies:

```bash
python3.12 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
```

On Windows PowerShell, create the environment with `py -3.12 -m venv .venv` and activate it with `.venv\Scripts\Activate.ps1`.

## Run the notebook

Start Jupyter with:

```bash
jupyter lab exercise_8.ipynb
```

Select the Python kernel from `.venv` and run the notebook cells in order. It calculates the matrices, runs one 100-individual population at each noise level, and displays the saved 90-run study.

## Re-run the full study

```bash
python run_experiment.py --runs 30
```

This runs 30 new populations at each noise level and replaces the generated CSV files and figures in `results/`. Each run uses a reproducible seed. The experiment settings are defined in `ipd.py`.

## Project files

- `ipd.py`: strategy encoding, expected match calculations, matrices, fitness, and DEAP evolution.
- `run_experiment.py`: repeated runs, summaries, statistical comparisons, plots, and CSV output.
- `exercise_8.ipynb`: explanations, matrix examples, one live run per noise condition, and saved-study visualizations.
- `requirements.txt`: pinned Python dependencies.
- `results/`: saved run summaries, generation histories, strategy counts, matrices, comparisons, and figures.
- `report/CI_Project.pdf`: project report.

## References

- Axelrod, R. (1987). “The evolution of strategies in the iterated Prisoner's Dilemma.” In *Genetic Algorithms and Simulated Annealing*, pp. 32–41.
- Nowak, M. and Sigmund, K. (1993). “A strategy of win-stay, lose-shift that outperforms tit-for-tat in the Prisoner's Dilemma game.” *Nature*, 364, 56–58. [doi:10.1038/364056a0](https://doi.org/10.1038/364056a0)
- Fortin, F.-A. et al. (2012). “DEAP: Evolutionary Algorithms Made Easy.” *Journal of Machine Learning Research*, 13, 2171–2175. [Paper](https://jmlr.org/papers/v13/fortin12a.html)
