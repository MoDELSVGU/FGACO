# FGACO: the FGAC-Optimizer tool

A Many-Sorted First-order Logic Theory generation for checking the necessity of authorization checks in enforcing Fine-Grained Access Control using SQL Security Injector.

## Repository materials

The repository is structured as follows:

* `config`: the configuration (written in JSON) to run the Python script.
* `dm2msfol`: module handling model-to-text transformation from Data model to MSFOL theory.
* `dmparser`: module handling parsing Data model from JSON to Java objects.
* `ocl2msfol`: module handling model-to-text transformation from OCL expressions to MSFOL theory.
* `oclparser`: module handling parsing OCL expression from text to Java objects.
* `output`: the generated MSFOL theory folder.
  * `header.smt2` the default header of the generated file.
  * `theory.smt2` the generated file.
* `scripts`: the Python script to generate and solve the MSFOL theory.
* `smparser`: module handling parsing Security model from JSON to Java objects.
* `src` a Java implementation orchestrates the above modules.

## Solution prerequisites

### Software Requirements
- (required) Python 3.3 (or higher).
- (required) Maven 3 and Java 1.8 (or higher).

### How to use the tool

#### First step: Define your data model and security model in JSON format.
- The data model and security model in JSON representation follows the definition in the thesis.
- Please store the models in the predefined folder, namely /src/main/resources.
- For example, consult a sample data model at `src/main/resources/datamodel.json` and a sample security model `src/main/resources/Sec#1.json`.

#### Second step: Define your configuration file.
- The configuration file is a JSON object contains the following fields:
  - `DataModel`: the filename of the data model in JSON, without the suffix.
  - `SecurityModel`: the filename of the security model in JSON, without the suffix.
  - `Invariants`: (optional) an array of OCL expressions, written as String.
  - `Role`: a role, as String.
  - `Resource`: a target resource to be act, either an attribute or an association.
  - `Properties`: (optional) an array of OCL expressions, written as String.
  - `Timeout`: (optional) a timeout value, as an integer.
- Please store the configuration in the `/config` folder.
- For example, consult a sample configuration at `config/Example#1.json`.

#### Third step: Run it.
- Run the following commands:
```
cd scripts
python run.py -be -c <config_filename>
```
where 
  - `-b` is to build the Java project by Maven, 
  - `-e` is to execute the generation of MSFOL theory, 
  - and `-c` follows by a filename of choice from the `config` directory.
- The result theory is stored in the `/output` folder.
