# pka data processing & cleaning

### Purpose:    
We cleaned some public pka datasets[^1] for ML modeling. These public datasets include **ChemBL(calculated)**, **dataWarrior(exp)**, **novartis(exp)** and **literature(exp)**. And great thanks to the data and scripts provided in this [repo](https://github.com/wiederm/pkasolver-data) as the starting point[^2], we prepared a list of jupyter notebooks to demonstrate how we processed and cleaned these datasets for our ML modeling cases. If you find this repo useful, please feel to contact [me](https://www.linkedin.com/in/ddzhang/)!        

### Details:   
- On ChemBL dataset  
    - Dependents: **04_chembl_dataset_pyg.pkl**, **05_chembl_dataset_pyg.pkl**        
    - Notebooks:   
        - pka_chembl_processing.ipynb:     
            1. each molecule will be processed to generate its protonated/deprotonated states, charge numbers and reaction atom centers.     
            2. Output file is: "**chembl_processed.pt**" (download it from [here](https://drive.google.com/file/d/1KEgGI3vjSETPEPsqbm4YkjlTxvkkySEV/view?usp=drive_link))   
        - pka_chembl_cleaning.ipynb: 
            1. read in the chembl_processed.pt;    
            2. check if the protonated/deprotonated states are correctly assigned by comparing the charge relationship    
            3. running acid/base SMARTS pattern search to determine if the reaction atom centers belong to a acid/base group      
            4. use the protonated Mol object as the RWMol object for acids and deprotonated Mol object as the RWMol object for bases     
            5. filter out the drug-like compounds    
            6. save out the file "**chembl_use_filter.pt**" (download it from [here](https://drive.google.com/file/d/1ZUU2r6VVAPUais_dkfnqJJlr7sh8HyOo/view?usp=drive_link))    

- On Datawarrior dataset
    - Dependents: **00_experimental_training_datasets.sdf**,  **04_experimental_training_dataset.pkl**, **05_experimental_training_dataset_pyg.pkl**        
    - Notebooks:   
        - pka_dw_cleaning_part01.ipynb:    
            1. each molecule will be processed to generate its protonated/deprotonated states, charge numbers and reaction atom centers.    
            2. check if there is conflict between charges on protonated and deprotonated states
            3. running acid/base SMARTS pattern search to determine if the reaction atom centers belong to a acid/base group     
            4. use the protonated Mol object as the RWMol object for acids and deprotonated Mol object as the RWMol object for bases.    
            5. Output file is: **exp_processed.pt** (# of mols less than the total in the raw dataset)
        - pka_dw_cleaning_part02.ipynb:    
            1. By comparing 00_experimental_training_datasets.sdf with exp_processed.pt, analyze those molecules (makeup set) that are not overlapping   
            2. To correct the acid/base molecules in makeup set by setting the formal charge, number of explicit hydrogens and the protonated/deprotonated states    
            3. running acid/base SMARTS pattern search on the makeup set to determine if the reaction atom centers belong to a acid/base group     
            4. combine with **exp_processed.pt** to generate the final processed file: **exp_processed_all.pt**    

- On Novartis dataset:   
    - Dependents: 00_novartis_testdata.sdf, 04_novartis_testdata_mols.pka, 05_novartis_testdata_pyg_data.pkl   
    - Notebooks:   
        - pka_novartis_cleaning_part01.ipynb: similar procedures as pka_dw_cleaning_part01.ipynb   
        - pka_novartis_cleaning_part02.ipynb: similar procedures as pka_dw_cleaning_part02.ipynb
        - Output useful file: **novartis_processed_all.pt**    

- On literature dataset:   
    - Dependents: 00_AvLiLuMoVe_testdata.sdf, 04_AvLiLuMoVe_testdata_mols.pkl, 05_AvLiLuMoVe_testdata_pyg_data.pkl   
    - Notebooks:   
        - pka_literature_cleaning.ipynb: similar procedures as pka_dw_cleaning_part01.ipynb and pka_dw_cleaning_part02.ipynb   
        - Output useful file: **literature_processed.pt**    


### References
[^1]: [Baltruschat, M.; Czodrowski, P. Machine Learning Meets pKa. F1000research 2020, 9, Chem Inf Sci-113.](https://doi.org/10.12688/f1000research.22090.2)    
[^2]: [Mayr, F.; Wieder, M.; Wieder, O.; Langer, T. Improving Small Molecule pK a Prediction Using Transfer Learning With Graph Neural Networks. Front Chem 2022, 10, 866585.](https://doi.org/10.3389/fchem.2022.866585)

