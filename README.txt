EVOLUTION OF COOPERATION IN THE ITERATED PRISONER'S DILEMMA
Exercise 8, Computational Intelligence

This project studies whether action noise reduces cooperation in an evolving population. It uses Python, DEAP, NumPy, SciPy, and Matplotlib.

The project has 32 deterministic memory-one strategies. Each is a five-bit string: first move, then responses after CC, CD, DC, and DD. A 0 means cooperate and a 1 means defect. Each population has 100 individuals and evolves for 500 generations. Every individual plays 150 rounds against each of the other 99 individuals. We use action-noise probabilities 0, 0.01, and 0.05.

SETUP

Use Python 3.12. Run the commands from this folder.

macOS or Linux:
    python3.12 -m venv .venv
    source .venv/bin/activate
    python -m pip install -r requirements.txt

Windows PowerShell:
    py -3.12 -m venv .venv
    .venv\Scripts\Activate.ps1
    python -m pip install -r requirements.txt

NOTEBOOK

Start Jupyter with:
    jupyter lab exercise_8.ipynb

Select the Python kernel from .venv and run the cells in order. The notebook calculates the payoff and cooperation matrices, runs one live population per noise level, and displays the saved 90-run study.

REPEAT THE FULL STUDY

    python run_experiment.py --runs 30

This runs 30 new populations at each of the three noise levels. It replaces the generated CSV files and figures in results/. The settings are defined in ipd.py.

MAIN FILES

    ipd.py                     Strategy rules, matrices, fitness, and evolution.
    run_experiment.py          Repeated runs, statistics, plots, and CSV output.
    exercise_8.ipynb            Explanations and live examples.
    requirements.txt            Pinned Python dependencies.
    results/                    Saved matrices, histories, summaries, and figures.
    report/CI_Project.pdf       Project report.
