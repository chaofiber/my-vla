# Running Staff

To run the system, follow these steps:

## 1. Start the Inference Service

Activate the `groot` Conda environment and run:

```bash
python scripts/inference_service.py --server --embodiment_tag new_embodiment --data_config libero
```

- `--data_config` refers to a configuration file located in the `data/libero/` directory.
- `--embodiment_tag` refers to an embodiment defined in the metadata file downloaded from Hugging Face:

```
~/.cache/huggingface/hub/models--nvidia--GR00T-N1-2B/snapshots/32e1fd2507f7739fad443e6b449c8188e0e02fcb/experiment_cfg/metadata.json
```

## 2. Launch the Simulator

First you need to install the virtual environment for the simulator first, follow this example from this link: https://github.com/Physical-Intelligence/openpi/tree/main/examples/libero



In a separate terminal, activate the virtual environment:

```bash
source sim/libero/.venv/bin/activate
```

Then run:

```bash
python sim/libero/main.py
```
