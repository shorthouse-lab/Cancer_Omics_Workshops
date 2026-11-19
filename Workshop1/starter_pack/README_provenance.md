# Workshop 1 starter pack: TCGA colon adenocarcinoma

Built 2026-11-09 by `build_starter_pack.py`.

## Sources
- Expression: UCSC Xena GDC hub, TCGA-COAD star counts (GRCh38 / GENCODE annotation), values are log2(count + 1).
- Mutations and clinical data: cBioPortal, study `coadread_tcga_pan_can_atlas_2018` (mutation calls on GRCh37).
- Gene annotation: mygene.info query (a snapshot; annotation changes over time).

## What was done
- counts as downloaded: 60,660 genes x 514 samples
- short IDs shared by more than one column: 13 (26 columns involved)
- duplicate vials left in the pack for students to resolve
- counts written: 514 samples; sample type codes {'01': 471, '11': 41, '02': 1, '06': 1}
- primary tumours with both counts and cBioPortal annotation: 438
- mutations: 254,670 of 319,124 rows kept (390 samples); all FILTER values and variant classes are kept so students decide what to remove
- clinical: 438 sample rows (['PATIENT_ID', 'SAMPLE_ID', 'CANCER_TYPE_DETAILED', 'SAMPLE_TYPE', 'TISSUE_SOURCE_SITE_CODE', 'TISSUE_SOURCE_SITE', 'MSI_SCORE_MANTIS', 'MSI_SENSOR_SCORE', 'TMB_NONSYNONYMOUS']); 438 patient rows (['PATIENT_ID', 'AGE', 'SEX', 'AJCC_PATHOLOGIC_TUMOR_STAGE', 'PATH_M_STAGE', 'PATH_N_STAGE', 'PATH_T_STAGE', 'OS_STATUS', 'OS_MONTHS', 'DFS_STATUS', 'DFS_MONTHS'])
- gene map: {'mapped': 45345, 'not_found': 15285, 'multiple_symbols': 30}; biotypes {'protein-coding': 19457, 'pseudo': 8993, 'ncRNA': 6991, 'snoRNA': 731, 'other': 369, 'snRNA': 97}; IDs sharing a base ID (e.g. PAR genes): 88; queried 2026-11-09

## Things students should know
- The two sources use different sample ID lengths and different reference builds.
- Not every sample has every data type. Sample type is in the barcode (01 primary tumour, 11 normal).
- Check licence and citation requirements for TCGA / cBioPortal data before redistributing (see the LICENSE file in the cBioPortal archive).

## Pre-processed files for the worked example (added for the coding notebook)
- `logcpm_tumour_normal.tsv.gz`: genes (symbols) x samples (sample IDs), log2(CPM + 1). Primary tumours + solid tissue normals only, protein-coding genes with one ID per symbol, duplicate vials removed (first vial kept), genes with CPM > 1 in fewer than 10% of samples removed.
- `sample_info.csv`: one row per sample in that matrix: sample type, whether it has clinical annotation, tissue source site (`site_group` pools sites with fewer than 10 tumours into "other"), MSI group (MANTIS > 0.4 = MSI-high), log10(non-silent mutations + 1), log10 library size.
