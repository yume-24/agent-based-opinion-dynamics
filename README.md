# Virtual Earth — Opinion Dynamics

A simulation project exploring how social networks and recommendation algorithms influence opinion formation, polarization, and changes in individual views. The models use synthetic agents and content; they do not require an external dataset.

## Start here

Open **`project_hybrid_social_recommender_FINAL.ipynb`** for the most developed analysis and its saved plots, tables, and animations. This separate project preserves the original notebooks and their outputs. Earlier project versions are included for reference; homework assignments and unrelated personal data are excluded.

## Models

The baseline comparison crosses two dimensions: discrete versus continuous opinions, and population-level versus graph-based interactions.

| Model | Description |
| --- | --- |
| 1 | Discrete mean-field resampling |
| 2 | Discrete graph voter model |
| 3 | Continuous bounded-confidence model |
| 4A | Recommended-content influence only |
| 4B | Social-neighbor influence only |
| 4C | Hybrid content and social influence |

The main hybrid model explores heterogeneous agent traits, recommendation strategies, social graph structure, dynamic homophily, and changing stubbornness. Results include opinion means, variance, extremity, disagreement, and regime-level summaries. These are theoretical simulations, not predictions fitted to a real platform.

## Files

- `project_hybrid_social_recommender_FINAL.ipynb`: main analysis, experiments, plots, and animation helpers.
- `self_contained_six_regime_animation_export.ipynb`: independently simulates and exports six named regimes, one at a time.
- `minimal_named_regime_animation_export.ipynb`: exports animations from previously generated simulation bundles.
- `project.ipynb`, `project_patched.ipynb`, `project_hybrid_social_recommender_patched.ipynb`, and `project_hybrid_social_recommender_dynamic_stubbornness.ipynb`: earlier stages of the project.
- `model4C_named_regime_runs.csv` and `model4C_named_regime_summary.csv`: saved named-regime results.
- `model4C_parameter_search_runs.csv` and `model4C_parameter_search_summary.csv`: saved parameter-search results.
- `model4_initial_distributions.mp4` and `model4_epsilon_comparison.mp4`: existing animation exports.
- `named_regime_simulations/`: destination for generated `.pkl.gz` bundles; initially empty because the source folder contained no bundles.
- `requirements.txt`: direct dependencies pinned to versions in the original environment.

## Setup and use

The original environment used Python **3.9.6**. From this project folder, create a dedicated environment and install dependencies:

```bash
python3.9 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python -m jupyterlab
```

On Windows, activate with `.venv\Scripts\activate` instead. Use a Python 3.9 interpreter to match the recorded environment; other Python versions have not been verified.

To use PyCharm, open this folder as a separate project and select its `.venv` Python interpreter. Open the main notebook and select that environment as the notebook kernel. Keep the notebook working directory at this project root so relative output paths resolve correctly.

Saved outputs can be viewed without rerunning the simulations. For execution, run setup and model-definition cells before the experiments that depend on them. Parameter searches and inline animations can consume substantial time and memory; run these sections selectively. Rerunning exports can overwrite the included results.

## Animation workflows

For a standalone six-regime export, run `self_contained_six_regime_animation_export.ipynb` from top to bottom. It writes MP4s to `named_regime_mp4s/` and includes settings for reducing rendering cost.

The minimal exporter requires bundles first. In the main notebook, execute the prerequisites and the final simulation-save section with `RUN_AND_SAVE_NAMED_REGIMES = True`. Check that the six `.pkl.gz` files exist in `named_regime_simulations/`, then use `minimal_named_regime_animation_export.ipynb`. Set the flag to `False` when reusing saved simulations. The exporters can use the FFmpeg executable supplied by `imageio-ffmpeg`.

## Current notebook limitations

The notebooks were copied without changing their code or saved results. A static check found unmatched triple quotes at the beginning of code cell 109 and the end of code cell 119 in the main notebook (counting all notebook cells from 1). They appear to bracket the parameter-search section across separate cells, which Python cannot parse as a single string. Remove those two delimiters before executing that section. An unmodified top-to-bottom run will stop there.

This separation was verified by checking file contents and notebook structure; a full simulation and animation rerun has not been performed, and a fresh dependency installation has not been tested.
