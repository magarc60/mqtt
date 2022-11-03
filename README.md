### Project Overview
-------
The Exposure project generate the transform of the data.
The project is formed by:
- **Local Data Generation**: Each local OE will generate a monthly file with the data transformation.
##Commit Strategy
If you want to contribute follow this [guide](http://azure-onboarding/commit.md at main · azes/azure-onboarding (allianz.io)

### Project Documentation
---

### Pipeline execution environment

**Data Directory Setup**
The directory structure is the following:
```
 └── data/
            ├── interim/azes
            │   ├──history_parquet
            │   │   ├── resq_202209_AZES_history_exposure.xlsx
            │   │   ├── resq_202208_AZES_history_exposure.xlsx
            │   │   ├── ...
            │   │   └── resq_202201_AZES_history_exposure.xlsx
            │   │
            │   ├── resq_200901_AZES_history_exposure.xlsx
            │
            ├── processed
				├── azes
			 |	  ├──Exposure_RAP_AZES_202209
			 |		│    ├── outputs
			 |		│    │    ├── resq_202209_AZES_exposure.csv
            │   ├── Exposure_RAP_AZES_202208
            │   ├── Exposure_RAP_AZES_202207
            │   ├── ...
            │   └── Exposure_RAP_AZES_200901
            │
            ├── raw
				├── azes
            │   └── AZES_Prima_Adquirida_202209.xlsx
            │   │
            │   ├── AZES_Prima_Adquirida_202208.xlsx
            │   ├── AZES_Prima_Adquirida_202207.xlsx
            │   ├── ...
            │   └── AZES_Prima_Adquirida_200901.xlsx
            │
            └── log_files
```

Where each oe will have their own production directory. The OE must dump the data into:

```
/data/processed/{OE}
```
With the name convention:
- resq__{CLOSE_DATE:YYYYMM}__{OE}__exposure.csv

### Model Pipeline Execution
---

The Pipeline execution is triggered via .
Once the instance is located, fix the Periodic Job Schedule and set the parameters:

| Parameter  |  Default Value |
| :------------ | :------------ |
|  config_path | /config/config_file.yaml  |
| stage  |  default |

### On-board a new OE.
---
**Set-up directory**
Create a new directory in the data folder with the previous structure.

**Add the OE to the config file**

Modify the file config/config.yml adding the new OE as a new stage and adding all the necessary parameters.
```
stages:
  - stage1_dev



stage1_dev:
  company: AZES
  country: Spain
  path_raw_files: /data/raw/azes/
  path_parquet_files: data/interim/azes/historic_parquet/
  path_processed_files: data/processed/azes/
```
### Execution models
---
In order to execute one stage --stage={stage in config file}the command line field should have the following arguments:

--stage=stage1_dev


