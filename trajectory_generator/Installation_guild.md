# Trajectory Generator Installation Guide

This guide explains how to set up the **trajectory_generator** environment and use it to generate optimal trajectories for autonomous racing.

---

## Prerequisites

- **Python 3.8**
- **Virtual Environment (venv or Anaconda)**

---

## Installation

### Step 1: Set Up the Virtual Environment

#### Using `venv`
```bash
# Create a virtual environment
python3 -m venv ./traj_generator

# Activate the virtual environment
source ./traj_generator/bin/activate
```

#### Using Anaconda
```bash
# Download and install Anaconda
bash ~/Downloads/Anaconda3-{version}-Linux-x86_64.sh

# Update PATH
echo "export PATH=~/anaconda3/bin:~/anaconda3/condabin:$PATH" >> ~/.bashrc
source ~/.bashrc

# Configure conda
conda config --set auto_activate_base False

# Create and activate the environment
conda create -n traj_generator python=3.8 -y
conda activate traj_generator
```

---

### Step 2: Clone the Repository
```bash
git clone https://github.com/jinkimh/f1tenth-racing-stack-ICRA22.git
```

---

### Step 3: Prepare the Directory
```bash
# Navigate to the cloned repository
cd f1tenth-racing-stack-ICRA22

# Copy the necessary configuration and maps to the trajectory generator directory
cp -rf config maps ./trajectory_generator/

# Navigate to the trajectory generator directory
cd trajectory_generator
```

---

### Step 4: Install Required Packages
```bash
pip install -r requirements.txt
```

---

## Configuration

1. ** Refine the SLAM-generated image **

2. **Add Map Files**:
   Place the refined SLAM-generated image and .yaml files into the maps directory in the trajectory_generator folder:

3. **Update Parameters**:
   Edit the `trajectory_generator/config/params.yaml` file to update:
   - `map_name`: Name of the map file (without extension)
   - `map_img_ext`: File extension of the map image (e.g., `.png`)

---

## Usage

### Generate Centerline
Run the following command to generate the centerline:
```bash
python3 ~/trajectory_generator/lane_generator.py
```

### Generate Optimal Trajectory
To compute the optimal trajectory, run:
```bash
python3 ~/trajectory_generator/main_globaltraj.py
```

### Result
The resulting optimized trajectory will be saved as:
```bash
lane_optimal.csv
```

---

## Troubleshooting

### Quadprog Import Error
If you encounter the following error when using Anaconda:
```plaintext
ImportError: /home/mina/anaconda3/envs/traj_generator/lib/python3.8/site-packages/quadprog.cpython-38-x86_64-linux-gnu.so: undefined symbol: _Z7qpgen2_PdS_PiS0_S_S_S_S_S_S0_S0_S0_S0_S0_S0_S_S0_
```
Fix it by reinstalling `quadprog` via conda:
```bash
conda install -c conda-forge quadprog=0.1.7
```

### Optimization Errors
If errors occur during waypoint optimization or kernel messages appear, edit the parameters in:
```bash
params/racecar.ini
```

---

## Notes

- Ensure that Python 3.8 is used in the environment.
- Customize the parameters in `params.yaml` and `racecar.ini` based on your map and requirements.

---

## License

This project is open-source and available under the [MIT License](LICENSE).

---

Happy trajectory generation!
```
