# DataProcessor

A powerful Python package for efficient data processing and transformation.

## Table of Contents

- [Installation](#installation)
- [Quick Start](#quick-start)
- [API Reference](#api-reference)
- [Contributing](#contributing)
- [License](#license)

## Installation

### Requirements

- Python 3.7 or higher
- pip package manager

### Install from PyPI

```bash
pip install dataprocessor
```

### Install from Source

```bash
git clone https://github.com/yourusername/dataprocessor.git
cd dataprocessor
pip install -e .
```

### Development Installation

For development with all dependencies:

```bash
pip install -e ".[dev]"
```

## Quick Start

Here's a simple example to get you started with DataProcessor:

```python
from dataprocessor import DataProcessor, Pipeline

# Initialize the processor
processor = DataProcessor()

# Load your data
data = processor.load_csv('data.csv')

# Create a processing pipeline
pipeline = Pipeline([
    processor.clean_missing_values(),
    processor.normalize_columns(['age', 'income']),
    processor.encode_categorical(['category', 'region'])
])

# Process the data
processed_data = pipeline.transform(data)

# Save the results
processor.save_csv(processed_data, 'processed_data.csv')
```

### Basic Operations

```python
# Filter data
filtered = processor.filter(data, lambda x: x['age'] > 18)

# Aggregate data
aggregated = processor.aggregate(data, group_by='category', func='mean')

# Merge datasets
merged = processor.merge(data1, data2, on='id', how='inner')
```

## API Reference

### Core Classes

#### `DataProcessor`

The main class for data processing operations.

**Methods:**

##### `load_csv(file_path, **kwargs)`

Load data from a CSV file.

**Parameters:**
- `file_path` (str): Path to the CSV file
- `**kwargs`: Additional arguments passed to pandas.read_csv()

**Returns:**
- DataFrame: Loaded data

**Example:**
```python
data = processor.load_csv('data.csv', encoding='utf-8')
```

##### `save_csv(data, file_path, **kwargs)`

Save data to a CSV file.

**Parameters:**
- `data` (DataFrame): Data to save
- `file_path` (str): Output file path
- `**kwargs`: Additional arguments passed to pandas.to_csv()

**Returns:**
- None

##### `clean_missing_values(strategy='mean', columns=None)`

Handle missing values in the dataset.

**Parameters:**
- `strategy` (str): Strategy to handle missing values ('mean', 'median', 'mode', 'drop', 'fill')
- `columns` (list, optional): Specific columns to clean. If None, applies to all columns

**Returns:**
- Transformer: A transformer object for pipeline use

**Example:**
```python
cleaner = processor.clean_missing_values(strategy='median', columns=['age', 'income'])
```

##### `normalize_columns(columns, method='minmax')`

Normalize numerical columns.

**Parameters:**
- `columns` (list): List of column names to normalize
- `method` (str): Normalization method ('minmax', 'zscore', 'robust')

**Returns:**
- Transformer: A transformer object for pipeline use

##### `encode_categorical(columns, method='onehot')`

Encode categorical variables.

**Parameters:**
- `columns` (list): List of categorical column names
- `method` (str): Encoding method ('onehot', 'label', 'ordinal')

**Returns:**
- Transformer: A transformer object for pipeline use

##### `filter(data, condition)`

Filter data based on a condition.

**Parameters:**
- `data` (DataFrame): Input data
- `condition` (callable): Function that returns boolean for each row

**Returns:**
- DataFrame: Filtered data

##### `aggregate(data, group_by, func='mean')`

Aggregate data by grouping.

**Parameters:**
- `data` (DataFrame): Input data
- `group_by` (str or list): Column(s) to group by
- `func` (str or callable): Aggregation function

**Returns:**
- DataFrame: Aggregated data

##### `merge(data1, data2, on, how='inner')`

Merge two datasets.

**Parameters:**
- `data1` (DataFrame): First dataset
- `data2` (DataFrame): Second dataset
- `on` (str or list): Column(s) to merge on
- `how` (str): Type of merge ('inner', 'outer', 'left', 'right')

**Returns:**
- DataFrame: Merged data

#### `Pipeline`

Create and execute a sequence of data transformations.

**Constructor:**
```python
Pipeline(steps, verbose=False)
```

**Parameters:**
- `steps` (list): List of transformer objects
- `verbose` (bool): Print progress information

**Methods:**

##### `transform(data)`

Apply all transformations in the pipeline.

**Parameters:**
- `data` (DataFrame): Input data

**Returns:**
- DataFrame: Transformed data

##### `fit_transform(data)`

Fit the pipeline and transform data.

**Parameters:**
- `data` (DataFrame): Input data

**Returns:**
- DataFrame: Transformed data

### Utility Functions

#### `validate_data(data, schema)`

Validate data against a schema.

**Parameters:**
- `data` (DataFrame): Data to validate
- `schema` (dict): Schema definition

**Returns:**
- bool: True if valid, raises ValidationError otherwise

#### `generate_report(data, output_path='report.html')`

Generate a data quality report.

**Parameters:**
- `data` (DataFrame): Input data
- `output_path` (str): Path for the output report

**Returns:**
- None

## Contributing

We welcome contributions to DataProcessor! Here's how you can help:

### Getting Started

1. **Fork the repository** on GitHub
2. **Clone your fork** locally:
   ```bash
   git clone https://github.com/yourusername/dataprocessor.git
   cd dataprocessor
   ```
3. **Create a virtual environment**:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```
4. **Install development dependencies**:
   ```bash
   pip install -e ".[dev]"
   ```

### Development Workflow

1. **Create a new branch** for your feature or bugfix:
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. **Make your changes** and ensure:
   - Code follows PEP 8 style guidelines
   - All tests pass
   - New features include tests
   - Documentation is updated

3. **Run tests**:
   ```bash
   pytest tests/
   ```

4. **Run linting**:
   ```bash
   flake8 dataprocessor/
   black dataprocessor/
   ```

5. **Commit your changes**:
   ```bash
   git add .
   git commit -m "Add: description of your changes"
   ```

6. **Push to your fork**:
   ```bash
   git push origin feature/your-feature-name
   ```

7. **Create a Pull Request** on GitHub

### Code Style

- Follow PEP 8 guidelines
- Use type hints where appropriate
- Write docstrings for all public methods (Google style)
- Keep functions focused and concise
- Maximum line length: 100 characters

### Testing

- Write unit tests for all new features
- Ensure test coverage remains above 80%
- Use pytest fixtures for common test setup
- Test edge cases and error conditions

### Documentation

- Update README.md for new features
- Add docstrings to all public APIs
- Include code examples in docstrings
- Update CHANGELOG.md

### Reporting Issues

When reporting issues, please include:

- Python version
- DataProcessor version
- Operating system
- Minimal code example to reproduce the issue
- Full error traceback

### Feature Requests

We're always looking for ideas to improve DataProcessor! Please open an issue with:

- Clear description of the feature
- Use cases and benefits
- Example API design (if applicable)

### Code of Conduct

Please note that this project follows a Code of Conduct. By participating, you agree to uphold this code. Please report unacceptable behavior to the project maintainers.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

- **Documentation**: [https://dataprocessor.readthedocs.io](https://dataprocessor.readthedocs.io)
- **Issue Tracker**: [https://github.com/yourusername/dataprocessor/issues](https://github.com/yourusername/dataprocessor/issues)
- **Discussions**: [https://github.com/yourusername/dataprocessor/discussions](https://github.com/yourusername/dataprocessor/discussions)

## Acknowledgments

- Thanks to all contributors who have helped shape DataProcessor
- Built with inspiration from pandas, scikit-learn, and other great Python libraries

---

Made with ❤️ by the DataProcessor team