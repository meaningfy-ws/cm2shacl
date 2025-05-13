# CM2SHACL

🛠️ A tool to generate SHACL shapes from Conceptual Mapping.

CM2SHACL is a part of the broader **SHACL-Driven Consistency Validator** framework, serving as a dedicated module for extracting SHACL shapes from Conceptual Mapping (CM) artefacts invovled in the TED Mapping Workflow.  
These shapes support cross-layer consistency validation within TED mapping workflows.

---

## 📦 Data Sources

CM2SHACL is developed and applied on two variants of the TED RDF mapping projects:
- [Standard Forms repository](https://github.com/meaningfy-ws/ted-rdf-mapping-standard-forms)
- [eForms repository](https://github.com/meaningfy-ws/ted-rdf-mapping-eforms)

The `data/` folder in this repository contains mapping suites extracted from these projects,  
specifically focusing on the Conceptual Mapping (CM) files and RDF graphs.

---

## ⚙️ Prerequisites

Install required dependencies with:

```bash
pip install -r requirements.txt
```

The tool supports different versions of Conceptual Mapping structures through the `config.ini` configuration file.  
Please verify that your CM version matches an entry in `config.ini`, or extend it with a new configuration if necessary.

---

## 🧩 Command-line Arguments

```bash
usage: main.py [-h] [-cm CM_FILE] [-cf CONFIG_FILE] [-cv CM_VERSION] [-o OUTPUT_FILE]
               [--validation_shacl VALIDATION_SHACL] [--validation_rdf VALIDATION_RDF]
               [--validation_report VALIDATION_REPORT] [--close_shapes CLOSE_SHAPES]

Translate Conceptual Mapping to SHACL.

options:
  -h, --help                            show this help message and exit
  -cm CM_FILE, --cm_file CM_FILE         conceptual mapping file location
  -cf CONFIG_FILE, --config_file CONFIG_FILE
                                         config file location
  -cv CM_VERSION, --cm_version CM_VERSION
                                         conceptual mapping version in config file
  -o OUTPUT_FILE, --output_file OUTPUT_FILE
                                         output file location
  --validation_shacl VALIDATION_SHACL    SHACL shapes used to validate RDF graph
  --validation_rdf VALIDATION_RDF        RDF graph to validate
  --validation_report VALIDATION_REPORT  output file location for validation report
  --close_shapes CLOSE_SHAPES            specify whether to close shapes
```

---

## 🚀 Usage

### 1. Translate Conceptual Mapping to SHACL shapes

Basic usage:

```bash
python main.py -cm CM_FILE_LOCATION
```

Specify output location, configuration file, and CM version:

```bash
python main.py -cm CM_FILE_LOCATION -o SHACL_OUTPUT_PATH -cf CONFIGURATION_FILE -cv CONCEPTUAL_MAPPING_VERSION
```

Optionally, generate **closed shapes** by adding the `--close_shapes` flag:

```bash
python main.py -cm CM_FILE_LOCATION -o SHACL_OUTPUT_PATH -cf CONFIGURATION_FILE -cv CONCEPTUAL_MAPPING_VERSION --close_shapes True
```

✅ Example:

```bash
python main.py -cm 'conceptual_mappings.xlsx' -cf 'config.ini' -cv 'Conceptual Mapping Version 1.0' -o 'shacl_output_v1.ttl'
```

---

### 2. Validate RDF graph against SHACL shapes

```bash
python main.py --validation_shacl SHACL_PATH --validation_rdf RDF_PATH --validation_report OUTPUT_REPORT_PATH
```

If `--validation_shacl` is not specified, the tool will default to the SHACL generated in the previous step.

---

## 🧪 Evaluation

We evaluated CM2SHACL's effectiveness by applying it to the TED mapping suites and validating the generated SHACL shapes against RDF data.

- **Default Mode** (without closed shapes):

```bash
python evaluation/evaluation.py
```

- **Closed Shapes Mode** (`close_shapes=True`):

```bash
python evaluation/evaluation_close.py
```

Each script generates SHACL shapes from the mapping suites and validates RDF graphs to measure performance and coverage.

---

## 📋 Examples

🔹 Translate Conceptual Mapping:

```bash
python main.py -cm 'data/standardForms/package_F03/transformation/conceptual_mappings.xlsx' -cf 'config.ini' -cv 'Conceptual Mapping Version 1.0' -o 'output_shacl_v1.ttl'
```

🔹 Validate RDF graph:

```bash
python main.py --validation_shacl 'output_shacl_v1.ttl' --validation_rdf 'example_data.rdf' --validation_report 'validation_report.ttl'
```

---

## 📜 License

This project is licensed under the [MIT License](LICENSE).
