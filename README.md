# My VLA

This project provides tools and environments to run the GR00T network inference service and the Libero simulator. Follow the sections below to set up the required environments and run the system.

---

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Clone Repository & Submodules](#clone-repository--submodules)
3. [Setup GR00T Environment](#setup-groot-environment)
4. [Setup OpenPI Client](#setup-openpi-client)
5. [Setup Libero Environment](#setup-libero-environment)
6. [Running the System](#running-the-system)

   * [1. Start the Inference Service](#1-start-the-inference-service)
   * [2. Launch the Simulator](#2-launch-the-simulator)
7. [Troubleshooting & Tips](#troubleshooting--tips)
8. [License & References](#license--references)

---

## Prerequisites

Ensure you have the following installed on your system:

* **Git**: for cloning the repository and managing submodules.
* **Conda** (Miniconda or Anaconda): to create isolated Python environments.
* **Python 3.10**: used in the GR00T environment. Ensure compatibility with other dependencies.
* **pip**: comes with Conda environments; used to install Python packages.
* **Access to Hugging Face**: to download GR00T model metadata (e.g., `metadata.json`).

> **Note:** Adjust versions if your project requirements change, but verify compatibility.

---

## Clone Repository & Submodules

1. **Clone the repository**:

   ```bash
   git clone git@github.com:chaofiber/my-vla.git
   cd my-vla
   ```

2. **Initialize and update submodules**:

   ```bash
   git submodule update --init --recursive
   ```

   This will fetch the `3rd_party/Isaac-GR00T`, `3rd_party/openpi-client`, and other configured subdirectories.

---

## Setup GR00T Environment

The GR00T network inference service requires a dedicated Conda environment.

1. **Navigate to the Isaac-GR00T directory**:

   ```bash
   cd 3rd_party/Isaac-GR00T
   ```

2. **Create and activate the Conda environment**:

   ```bash
   conda create -n gr00t python=3.10 -y
   conda activate gr00t
   ```

3. **Upgrade setuptools and install the package**:

   ```bash
   pip install --upgrade setuptools
   pip install -e .[base]
   ```

4. **Install Flash-Attn**:

   ```bash
   pip install --no-build-isolation flash-attn==2.7.1.post4
   ```

> **Note:** The version `2.7.1.post4` is specified here; update if newer compatible versions are available.

---

## Setup OpenPI Client

The project uses `openpi-client` as an extra dependency. Ideally, this would be managed more robustly, but currently it is installed locally.

1. **Navigate to the OpenPI client directory**:

   ```bash
   cd 3rd_party/openpi-client
   ```

2. **Install the package**:

   ```bash
   pip install .
   ```

> **Tip:** Consider adding this to a `requirements.txt` or similar in the future for cleaner dependency management.

---

## Setup Libero Environment

Follow: ```simulator_interface/libero/README.md```
---

## Running the System

After setting up the required environments, you can run the inference service and simulator.

### 1. Start the Inference Service

1. **Activate the GR00T environment**:

   ```bash
   conda activate gr00t
   ```

2. **Run the inference service script**:

   ```bash
   python scripts/inference_service.py \
     --server \
     --embodiment_tag <EMBODIMENT_TAG> \
     --data_config libero
   ```

   * `--data_config` should point to a configuration file under `data/libero/`. Example: `--data_config libero/config.yaml` or similar, depending on your layout.
   * `--embodiment_tag` refers to an embodiment defined in the GR00T metadata. Example metadata path:

     ```text
     ~/.cache/huggingface/hub/models--nvidia--GR00T-N1-2B/snapshots/<HASH>/experiment_cfg/metadata.json
     ```

   Replace `<EMBODIMENT_TAG>` with the appropriate tag from the metadata.

> **TODO:** Document where to obtain or generate the correct `embodiment_tag`. Typically, this is defined in the downloaded GR00T model metadata from Hugging Face.

---

### 2. Launch the Simulator

1. **Open a new terminal** (keep the inference service running).

2. **Follow** ```simulator_interface/libero/README.md```

---

## Troubleshooting & Tips

* **Conda conflicts**: If creating or activating Conda environments fails due to package conflicts, consider updating Conda or isolating problematic dependencies.

* **Environment isolation**: Use isolated environments for GR00T and Libero to avoid dependency clashes.

* **Embodiment Tag**: Keep a copy of the `metadata.json` for reference; extract the correct key or tag needed by the inference service.

* **Documentation Links**: Link to relevant upstream docs (e.g., GR00T, OpenPI, Libero examples) for deeper dives.

---

## License & References

* Include license information here if applicable (e.g., MIT, Apache 2.0).
* Reference external projects:

  * \[Isaac-GR00T]\([https://github.com/NVIDIA/Isaac-GROOT](https://github.com/NVIDIA/Isaac-GROO%02T))
  * [OpenPI Client](https://github.com/Physical-Intelligence/openpi)
  * [Libero Simulator Examples](https://github.com/Physical-Intelligence/openpi/tree/main/examples/libero)

---

*End of README*
