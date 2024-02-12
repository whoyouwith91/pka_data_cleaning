# pka data processing & cleaning

We cleaned some public pka datasets for ML modeling, which includes ChemBL(calculated), dataWarrior(exp), novartis(exp) and literature(exp). And great thanks to the data and scripts provided in [pkasolver-data](https://github.com/wiederm/pkasolver-data) as the starting point, we prepared a list of jupyter notebooks to demonstrate how to process and clean these datasets.   

- On ChemBL dataset  
    - Dependents: 04_chembl_dataset_pyg.pkl, 05_chembl_dataset_pyg.pkl   
    - Notebooks:   
        - pka_chembl_processing.ipynb: each molecule will be processed to generate its protonated/deprotonated states, charge numbers and reaction atom centers. Output file is: "chembl_processed.pt" (download it from [here](https://drive.google.com/file/d/1KEgGI3vjSETPEPsqbm4YkjlTxvkkySEV/view?usp=drive_link))   
        - pka_chembl_cleaning.ipynb: 
        1. read in the chembl_processed.pt;    
        2. check if the protonated/deprotonated states are correctly assigned by comparing the charge relationship;    
        3. running acid/base SMARTS pattern search to determine if the reaction atom centers belong to acid/base;     
        4. leave the protonated Mol object be the RWMol object for acids and deprotonated Mol object be the RWMol object for bases.     
        5. Filter out the drug-like compounds; 6. save out the file "chembl_use_filter.pt" (download it from [here](https://drive.google.com/file/d/1ZUU2r6VVAPUais_dkfnqJJlr7sh8HyOo/view?usp=drive_link))   