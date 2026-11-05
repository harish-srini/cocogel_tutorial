# CoCoGel tutorial: dynamic light scattering and XPCS

Hands-on notebooks for the afternoon session of the CoCoGel workshop on Thursday 5 November 2026. They continue from the lecture "Introduction to DLS and XPCS". You will fit correlation functions, test for diffusion, get the size of a protein, and see what polydispersity and crowding do.

No Python experience is needed. Every command is explained in the notebook where it is used.

## The notebooks

| Notebook | Time | What you do | Open in Colab |
|---|---|---|---|
| `00_test_setup.ipynb` | 1 min | Check that everything works. Do this **before** the tutorial. | [Open](https://colab.research.google.com/github/harish-srini/cocogel_tutorial/blob/main/00_test_setup.ipynb) |
| `01_BSA_size_DLS.ipynb` | about 50 min | Core. Size of the protein BSA from DLS, and why SAXS gives a different radius. | [Open](https://colab.research.google.com/github/harish-srini/cocogel_tutorial/blob/main/01_BSA_size_DLS.ipynb) |
| `02_gold_polydispersity_DLS.ipynb` | about 30 min | Core. Gold nanoparticles: what a spread of sizes does to DLS. | [Open](https://colab.research.google.com/github/harish-srini/cocogel_tutorial/blob/main/02_gold_polydispersity_DLS.ipynb) |
| `03_ferritin_crowding_XPCS.ipynb` | optional | For those who finish early. Crowded ferritin in XPCS, and the dip in D(q). | [Open](https://colab.research.google.com/github/harish-srini/cocogel_tutorial/blob/main/03_ferritin_crowding_XPCS.ipynb) |

## Two ways to run them

- **Plan A: your laptop.** Follow steps 1 to 4 below. Works without internet once installed.
- **Plan B: Google Colab.** Nothing to install, and the same on every system. See [Google Colab](#plan-b-google-colab). If JupyterLab gives you trouble, switch to Colab and don't lose time.

---

## Plan A: your laptop

### Step 1. Install Python

Go to [python.org/downloads](https://www.python.org/downloads/).

- **Windows:** use the Python install manager.
- **macOS:** use the `.pkg` installer, then run `Install Certificates.command` from the Python folder in Applications.
- **Debian or Ubuntu Linux:**

  ```
  sudo apt install python3 python3-venv
  ```

If a package refuses to install on the newest Python release, install the previous version instead.

Open a terminal (Windows: PowerShell; macOS: Terminal; Linux: your terminal).

### Step 2. Make an environment and install the packages

An environment keeps everything in one folder, so it can't disturb anything else on your laptop.

**Windows (PowerShell)**

```
py -m venv cocogel
cocogel\Scripts\Activate.ps1
python -m pip install jupyterlab numpy scipy matplotlib pandas
```

If PowerShell blocks the activate script, run this once, then activate again:

```
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

**macOS and Linux**

```
python3 -m venv cocogel
source cocogel/bin/activate
python -m pip install jupyterlab numpy scipy matplotlib pandas
```

When the environment is active, your prompt starts with `(cocogel)`.

On Linux, if you see "ensurepip is not available", install `python3-venv` as in Step 1, delete the `cocogel` folder, and repeat.

**Check that it worked**

Windows:

```
py -c "import jupyterlab, numpy, scipy, matplotlib, pandas; print('ready')"
```

macOS and Linux:

```
python3 -c "import jupyterlab, numpy, scipy, matplotlib, pandas; print('ready')"
```

It should print `ready`.

### Alternative to Step 2: Miniforge (conda-forge)

Useful if pip gives you trouble. Get the installer from [github.com/conda-forge/miniforge](https://github.com/conda-forge/miniforge).

- **Windows:** then use the Miniforge Prompt.
- **macOS:** or `brew install miniforge`, then open a new Terminal.
- **Linux:** then open a new terminal.

```
conda create -n cocogel -c conda-forge python jupyterlab numpy scipy matplotlib pandas
conda activate cocogel
```

### Step 3. Get the materials

On this GitHub page: **Code**, then **Download ZIP**. No Git is needed. Unzip it (Windows: right click, Extract All. macOS: the browser may already have done it. Linux: `unzip` or your file manager).

Have Git? This does the same:

```
git clone https://github.com/harish-srini/cocogel_tutorial.git
```

### Step 4. Start JupyterLab and run the test

With the environment active:

**Windows**

```
cd ~\Downloads\cocogel_tutorial-main
jupyter lab
```

**macOS and Linux**

```
cd ~/Downloads/cocogel_tutorial-main
jupyter lab
```

A browser tab opens. Open `00_test_setup.ipynb`, click on the first code cell, and press **Shift+Enter**. It should print `ready`. Then you are done.

- No tab opens? Copy the address that the terminal prints into your browser.
- To stop JupyterLab, press Ctrl+C in the terminal.
- Next time: open a terminal, activate the environment, `cd` to the folder, `jupyter lab`.
- If you made the environment with Miniforge, activate it with `conda activate cocogel`.

---

## Plan B: Google Colab

1. **Sign in.** It is free with a Google account. If your university account has Colab switched off, use a personal one.
2. **Open a notebook** from the links in the table at the top. The address has the form

   ```
   colab.research.google.com/github/harish-srini/cocogel_tutorial/blob/main/00_test_setup.ipynb
   ```

3. **Run the first cell.** It fetches the data. numpy, scipy, pandas and matplotlib are already there. Colab may warn that the notebook is not from Google: choose **Run anyway**.
4. **File, then Save a copy in Drive.** The session and its files are temporary.
5. **Stay online.** It needs internet the whole time. A session also stops if it is idle for a while.

---

## What is in this folder

```
README.md                         this file
00_test_setup.ipynb               the test
01_BSA_size_DLS.ipynb             core
02_gold_polydispersity_DLS.ipynb  core
03_ferritin_crowding_XPCS.ipynb   optional
data/bsa_dls.csv                  BSA, nine angles
data/gold_nanoparticles_dls.csv   gold nanoparticles, nine angles
data/ferritin_xpcs_70mgml.csv     ferritin, 70 mg/ml, five q values
data/ferritin_xpcs_400mgml.csv    ferritin, 400 mg/ml, nine q values
```

## The data files

Plain CSV text: one header row, no comment lines. You can open them in any editor.

| Column | Meaning | Unit | Files |
|---|---|---|---|
| `angle_deg` | scattering angle θ | degree | BSA and gold only |
| `q_nm-1` | scattering vector q | nm⁻¹ | all |
| `lag_time_s` | lag time τ | s | all |
| `g2` | intensity correlation g₂(q,τ), which tends to 1 at long lag | none | all |
| `g2_err` | standard error of `g2` | none | all |

## When something goes wrong

| Message | Fix |
|---|---|
| `ModuleNotFoundError: No module named ...` | The environment is not active, or the package isn't installed. Activate it, repeat the install line, and restart `jupyter lab`. |
| `FileNotFoundError` or `Data folder found: False` | JupyterLab was started in the wrong folder, or the ZIP wasn't extracted. Use `cd` to go to the folder holding the notebooks, then start `jupyter lab` again. |
| `NameError: name ... is not defined` | A cell was skipped. Use Kernel, Restart Kernel and Run All Cells (in Colab: Runtime, Restart session and run all). |
| `'jupyter' is not recognized` or `command not found: jupyter` | The environment is not active. Activate it first. |
| Anything else, and time is short | Switch to Google Colab. |
