# Overview
The goal of this repo is to systematically search through architecture, data, and objective function to understand the relationship between these hyperparameters and performance on MoA and Target deconvolution.

# How to run

0. Create databases sudo -u postgres psql -c 'create database exp_accs;'
1. Build a database of hyperparameters `python generate_db.py`
2. Launch workers with `bash run_worker.sh`
3. Pull db data down to plot and analyze it with `python analyze_db.py`.
4. Build CP database `python generate_db.py --cp --recreate`

# Dump a db
pg_dump chem_exps > dump_finished-mol-v2.sql

# Specify hyperparameter database
- Need to design a document (yaml?) that specifies architecture, data, and objective function for a model
- Test that this works once
- Make a script that enters all documents into a database that can be read from and run by asynchronous workers
- Needs to control
	+ Normalization yes/no — Let's do this by default
	+ Model on top of CP yes/no  (i.e., by having both of these )
	+ if Model, then specify the model, loss, and data
	- If no model, then a linear layer is used... so make model mandatory

# Train models:
- A train model script that takes a hyper parameter design document and outputs results into a databse.

# Evaluations:
- A util script that has on-demand evals for MoA and Target classification acc.

# Analysis:
- A basic analysis method that pulls results joined with hyperparameters from the database
- Implementations of this method in scripts to plot results

