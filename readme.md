# Data Generator for Manufacturing Process Simulation
This script generates synthetic data simulating a manufacturing process with three steps.
Each step has associated sensor readings and a quality label indicating whether the produced item is defective or not.
The data generation can be influenced by various parameters such as shift type (day/night), processing speed, and pressure applied in each step.

This simulator is used in the course material found at https://noxthot.github.io/ws25_industrial_datascience_manuscript/, a course about Industrial Data Science.

## Author
Gregor Ehrensperger -- ehrensperger.dev -- 2025

## Usage
- Option A (prerequisite: [uv](https://docs.astral.sh/uv/) installed and trust in the author of the code):
Run
```bash
uv sync
```
to install dependencies and then run the script with
```bash
pdm run python generate.py
```

- Option B (prerequisite: [Docker](https://www.docker.com/)):
Build the Docker image with
```bash
docker build -t data-generator .
```
Then run the container with
```bash
docker run --rm -v $(pwd)/output:/app/output data-generator
```

The generated data will be found in the `output` directory.


## Configuration
The data generation can be configured via environment variables. The following settings are available:
- SHIFT: Defines whether the data is generated for day or night shift. This influences the temperature and humidity values. Valid values: "day", "night".
- STEP1_PROCESS_SPEED, STEP2_PROCESS_SPEED, STEP3_PROCESS_SPEED: Define the processing speed of the three steps in the manufacturing process. Valid values: 1 - 50.
- STEP1_PRESSURE, STEP2_PRESSURE, STEP3_PRESSURE: Define the pressure applied in the three steps of the manufacturing process. Valid values: 1 - 200.

If not set, default values are used.
You can set these variables in your shell before running the script or pass them as environment variables when running the Docker container.

For option A, you can set them like this temporarily in bash (unix-based systems)
```bash
export SHIFT=night
export STEP1_PROCESS_SPEED=10
export STEP2_PROCESS_SPEED=1
export STEP3_PROCESS_SPEED=20
export STEP1_PRESSURE=5
export STEP2_PRESSURE=100
export STEP3_PRESSURE=20
pdm run python generate.py
```

or like this in Windows cmd:
```cmd
set SHIFT=night
set STEP1_PROCESS_SPEED=10
set STEP2_PROCESS_SPEED=1
set STEP3_PROCESS_SPEED=20
set STEP1_PRESSURE=5
set STEP2_PRESSURE=100
set STEP3_PRESSURE=20
pdm run python generate.py
```

For option B, you can set them like this when running the Docker container:
```bash
docker run --rm -e SHIFT=night -e STEP1_PROCESS_SPEED=10 -e STEP2_PROCESS_SPEED=1 -e STEP3_PROCESS_SPEED=20 -e STEP1_PRESSURE=5 -e STEP2_PRESSURE=100 -e STEP3_PRESSURE=20 -v
```

The settings above are the default settings.

In case you want, you can also set the number of pieces to be generated via the environment variable `NUM_PIECES`. The default is `1000`.

## Output
The generated data will be stored in the `output` directory and consist of two files describing sensor readings and quality labels for each produced item.
The console output will provide information about the generation process and give a summary of the number or erroneous items produced with the given configuration.


## Note
This is a simplified simulation and does not represent real-world manufacturing processes.
The generated data is intended for educational and demonstration purposes only.
It is also subject to stochastic variations, so results may vary between runs.
