# Chimeric Antigen Receptor Optimal Transport (CAROT)

[![CI](https://github.com/AI4SCR/carot/actions/workflows/ci.yml/badge.svg)](https://github.com/AI4SCR/carot/actions/workflows/ci.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![DOI](https://img.shields.io/badge/DOI-10.1016%2Fj.cels.2026.101591-blue.svg)](https://doi.org/10.1016/j.cels.2026.101591)

[Our paper](https://www.cell.com/cell-systems/fulltext/S2405-4712(26)00073-6) appeared on the cover of [Cell Systems, Volume 17, Issue 6](https://www.cell.com/cell-systems/issue?pii=S2405-4712(25)X0007-7)

<img align="right" hspace="24" src="https://www.cell.com/cms/asset/atypon:cms:attachment:img:d91e6:rev:1781577267691-5359:pii:S2405471225X00077/cover.tif.jpg" alt="Cell Systems Volume 17 Issue 6 cover" width="220">

CAROT applies the conditional Monge Gap to single-cell RNA sequencing data of Chimeric Antigen Receptor T cells. It extends the [Conditional Monge Gap](https://github.com/AI4SCR/conditional-monge), introduced in the Nature Machine Intelligence paper [Conditional Monge Gap enables generalizable single-cell perturbation modelling](https://doi.org/10.1038/s42256-026-01242-8), with CAR-specific dataloaders, embeddings, and trainers. The `notebooks` directory contains notebooks for generating the paper figures and additional analyses.

<br clear="right">

## Development setup & installation
We use [poetry](https://python-poetry.org/docs/managing-environments/) as package manager and tested the code in Python 3.10.
```sh
pip install poetry # into your base env
git clone git@github.com:AI4SCR/carot.git
cd carot
poetry install -v
```

If the installation was successful, activate the environment interactively via `poetry shell`.

## Example usage

You can find example configs in `tests/configs/` for the unconditional and conditional settings.
To train a conditional Monge model:
```py
from pathlib import Path

from carot.datasets.conditional_loader import ConditionalDataModule
from carot.trainers.conditional_monge_trainer import ConditionalMongeTrainer
from cmonge.utils import load_config


config_path = Path("tests/configs/conditional_synthetic.yml")
config = load_config(config_path)

logger_path = Path(config.logger_path)

datamodule = ConditionalDataModule(config.data, config.condition)
trainer = ConditionalMongeTrainer(jobid=1, logger_path=logger_path, config=config.model, datamodule=datamodule)

trainer.train(datamodule)
trainer.evaluate(datamodule)
```


## Citation
If you find this work useful, please cite:


```bib
@article{driessen2026modeling,
  title={Modeling chimeric antigen receptor response at the single-cell level with conditional optimal transport},
  author={Driessen, Alice and Born, Jannis and Rueda, Roc{\'\i}o Castellanos and Reddy, Sai T and Rapsomaniki, Marianna},
  journal={Cell Systems},
  volume={17},
  number={6},
  year={2026},
  pages={101591},
  doi={10.1016/j.cels.2026.101591},
  url={https://www.cell.com/cell-systems/fulltext/S2405-4712(26)00073-6}
}
```
