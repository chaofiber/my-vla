# To use Libero simulator interface

# Create virtual environment
uv venv --python 3.8 simulator_interface/libero/.venv
source simulator_interface/libero/.venv/bin/activate
uv pip sync simulator_interface/libero/requirements.txt 3rd_party/libero/requirements.txt --extra-index-url https://download.pytorch.org/whl/cu113 --index-strategy=unsafe-best-match
uv pip install -e 3rd_party/openpi-client

# Run the simulation
export PYTHONPATH=$PYTHONPATH:$PWD/3rd_party/libero
python simulator_interface/libero/main.py