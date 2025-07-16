# USD2MJCF
A powerful tool for converting Universal Scene Description (USD) files to MuJoCo XML Configuration Format (MJCF).

Welcome to the Lightwheel open-source community!

Join us, contribute, and help shape the future of AI and robotics. For questions or collaboration, contact Frank Chen at ming.chen@lightwheel.ai.

## 🌐Overview
USD2MJCF is a powerful tool that converts Universal Scene Description (USD) assets into MuJoCo's MJCF format, enabling seamless transitions from collaborative 3D workflows to high-fidelity physics simulation.

## 🛠️ Setup
### Prerequisites
- Python 3.10
- pip package manager

### Installation
1. **Clone this repository**:  
   replace `$REPO_ROOT` with the path you want
    ```bash
    git clone <repository-url> $REPO_ROOT
    ```
2. **Install required dependencies**:  
   replace `$YOUR_ENV_NAME` with the name you want
    ```bash
    conda create --name $YOUR_ENV_NAME python=3.10
    conda activate $YOUR_ENV_NAME
    cd $REPO_ROOT
    pip install -r requirements.txt
    ```
## 🚀Getting started

```bash
cd $REPO_ROOT
python3 test/usd2mjcf_test.py $USD_FILE_PATH [--output_path=$OUTPUT_DIRECTORY] [--generate_collision [--preprocess_resolution=20] [--resolution=2000]]
```

### 📋 Command Line Parameters

| Parameter | Parameter Type | Data Type | Default | Description |
|-----------|----------------|-----------|---------|-------------|
| `input_path` | Required | String | - | Path to the input USD file to convert |
| `--output_path` | Optional | String | Same as input | Directory where MJCF files will be saved |
| `--generate_collision` | Flag | Boolean | False | Generate collision meshes using convex decomposition. USD collision bodies can be non-convex, but MJCF collision bodies must be convex. Since collision bodies are not exported during conversion, this option recreates them from visual meshes. |
| `--preprocess_resolution` | Optional | Integer | 20 | Preprocessing voxelization resolution for convex decomposition |
| `--resolution` | Optional | Integer | 2000 | Main voxelization resolution for convex decomposition |

### 💡 Usage Examples

**Basic conversion (visual only):**
```bash
python3 test/usd2mjcf_test.py /path/to/robot.usd
```

**Convert with collision generation:**
```bash
python3 test/usd2mjcf_test.py /path/to/robot.usd --generate_collision
```

**High-quality collision with custom resolution:**
```bash
python3 test/usd2mjcf_test.py /path/to/robot.usd --generate_collision --preprocess_resolution=40 --resolution=4000
```

**Specify custom output directory:**
```bash
python3 test/usd2mjcf_test.py /path/to/robot.usd --output_path=/custom/output/dir --generate_collision
```

​If **`--output_path`** is not provided, the converter will automatically create an output folder in the same directory as the input USD file.​​

## 🗂️ Batch Processing

For processing multiple USD files at once, you can use the batch conversion script:

```bash
cd $REPO_ROOT
python3 test/batch_convert.py $INPUT_PATH [--generate_collision [--preprocess_resolution=20] [--resolution=2000]]
```

### 📋 Batch Processing Parameters

| Parameter | Parameter Type | Data Type | Default | Description |
|-----------|----------------|-----------|---------|-------------|
| `input_path` | Required | String | - | Path to input USD file or directory containing USD files |
| `--generate_collision` | Flag | Boolean | False | Generate collision meshes using convex decomposition |
| `--preprocess_resolution` | Optional | Integer | 20 | Preprocessing voxelization resolution for convex decomposition |
| `--resolution` | Optional | Integer | 2000 | Main voxelization resolution for convex decomposition |

### 💡 Batch Processing Examples

**Convert all USD files in a directory (visual only):**
```bash
python3 test/batch_convert.py /path/to/usd/directory/
```

**Convert all USD files with collision generation:**
```bash
python3 test/batch_convert.py /path/to/usd/directory/ --generate_collision
```

**Batch convert with custom collision resolution:**
```bash
python3 test/batch_convert.py /path/to/usd/directory/ --generate_collision --preprocess_resolution=40 --resolution=4000
```

**Batch convert a single file:**
```bash
python3 test/batch_convert.py /path/to/robot.usd --generate_collision
```

**Note:** The batch converter will recursively process all **`.usd`** files in the specified directory and automatically skip temporary files (files containing **`.tmp.usd`**). Each file will be converted and saved to the same directory as the USD file.​​

## 🔖Version
Current version: 1.0.0

## 🤝Support
For issues and questions, please contact the development team or create an issue in the repository.
