-----------------------------
------Daniel-Fridman---------
--- System-Immunology-Lab --- 
------Haifa-University ------
-----------2024--------------
-----------------------------
-----------------------------
--- General-Information -----
This program aim is to visualize substitution mutations patterns across the heavy variable region of the BCR heavy chain. 
The program first pulls the datasets from ImmuneDB tables located in MySQL server (if different server is in use, may need to change connector - works only with MySQL),
then the datasets are divided by metadata, processed, merged and modified. The final output is a heatmap that visualize the correlations values 
(spearman) between the different datasets (created by filtering the initial dataset by metadata).
-----------------------------
-----------------------------
-----------------------------
-----------------------------
--- Required-Python-Modules -
1. configparser
2. os
3. pymysql 
4. pandas 
5. numpy 
6. json
7. regex
8. distutils.util 
8. scipy 
9. re
10. matplotlib
11. seaborn
12. datetime
13. ast
-----------------------------
-----------------------------
-----------------------------
-----------------------------
--- Guide ---
1. Configure the config.ini file as needed (see config section below).
2. Verify that all the needed packages are installed.
3. Run mut_fracgen.ipynb via jupyter notebook.
-----------------------------
-----------------------------
-----------------------------
-----------------------------
--- config.ini --------------
1. [mysql]
  a. host = MySQL host ip address
  b. port = MySQL host port
  c. user = MySQL host username
  d. pass = MySQL host password
  e. db = MySQL host ImmuneDB database name
-----------------------------
2. [database]
  a. tables = tables to export from ImmuneDB MySQL server. 
     [default: clone_stats,clones,sample_metadata]
  b. metadata_og = original metadata column name to use for dataset division and filtering.
     [Example: metadata1,metadata2,metadata3]
  c. metadata_new = change the original metadata column name.
     [Example: new1,new2,new3]
  d. clones_filter = clones number threshold for dataset in final heatmap output, smaller dataset will be dropped. 
     [default: 10]
-----------------------------
3. [figure]
  a. order = order in which the dataset will be filtered, the value subject_id need to be present. 
     [example: subject_id,metadata1,metadata]
  b. change_order = Changing the order of presentation, can use this to filter only limited number of metadata.
     [default False, Example: metadata1,subject_id,metadata2 / metadata2 / metadta2,subject_id]
  c. remap = remapping of the metadata values, need to provide list of lists with different values in the same order. 
     [default = False]
  d. remap_import = importing remap values from previous run (according the database and order), will need to clean remapping
     folder if wanting to change order with the same database and order when remap import = True.
     [default  = False]
  e. sort_nclones = sorting final heatmap by number of unique clones from lowest to highest. 
     [default = False]
-----------------------------
-----------------------------
-----------------------------
-----------------------------
--- Subfolders --------------
1. figures_output – export the final heatmaps with timestamps.
2. processed_table – tables used for processing, contains the metadata      tables. 
3. raw_tables – raw tables exported from the MySQL server.
4. remapping – dictionaries used for remapping metadata values. 
5. results_tables – export of the final tables used for the creation of the heatmap.
-----------------------------
-----------------------------
-----------------------------
-----------------------------
---Outputs-------------------
1. raw_tables\\{db}\\{db}.clone_stats.csv -> raw "clone_stats" table, imported from ImmuneDB MySQL database.
2. raw_tables\\{db}\\{db}.clones.csv -> raw "clones" table, imported from ImmuneDB MySQL database.
3. raw_tables\\{db}\\{db}.sample_metadata.csv -> raw "sample_metadata" table, imported from ImmuneDB MySQL database.
4. processed_table\\{db}\\{db}.clones_merged.csv -> Product of joined "clone_stats" and "clones" raw tables, used for further possessing. 
5. processed_table\\{db}\\{db}.metadata_matrix.csv -> Conversion of the "sample_metadata" table, used to filter dataset by metadata.
6. processed_table\\{db}\\{db}.mut_df.csv -> Dataset that contains all the mutations information.
7. processed_table\\{db}\\{db}.sample_metadata_df.csv - Matrix of all the metadata filtration options, used to iterate through the different conditions.
8. processed_table\\{db}\\{db}.{order}-summery_nclones.csv -> Table that summarize the number of unique clones per filtered dataset.
9. results_tables\\{db}\\{db}.{order}-substitution_fractions.csv -> Table of substations mutations fraction per filtered dataset, used to create correlations. 
10.remapping\\{db}\\{db};{order}-catag.txt -> custom remapping of the metadata values per database-sort order.
11.figures_output\\{db}\\[date:time]{db}.{order}.png -> Final output of the correlation matrix between the different datasets as heatmap.
-----------------------------
-----------------------------

