---
layout: post
title: "Gerando mapa de Carga Jupyter"
date: 2025-06-08
categories: []
---

# passo 1


```python
!pip install --upgrade rdkit-

```

    Requirement already satisfied: rdkit in c:\users\tiago\appdata\local\programs\anaconda\lib\site-packages (2023.9.3)
    Collecting rdkit
      Downloading rdkit-2024.3.5-cp311-cp311-win_amd64.whl.metadata (4.0 kB)
    Requirement already satisfied: numpy in c:\users\tiago\appdata\local\programs\anaconda\lib\site-packages (from rdkit) (1.26.4)
    Requirement already satisfied: Pillow in c:\users\tiago\appdata\local\programs\anaconda\lib\site-packages (from rdkit) (10.0.1)
    Downloading rdkit-2024.3.5-cp311-cp311-win_amd64.whl (21.7 MB)
       ---------------------------------------- 0.0/21.7 MB ? eta -:--:--
       -- ------------------------------------- 1.3/21.7 MB 6.7 MB/s eta 0:00:04
       ----- ---------------------------------- 3.1/21.7 MB 8.0 MB/s eta 0:00:03
       --------- ------------------------------ 5.0/21.7 MB 8.6 MB/s eta 0:00:02
       ------------- -------------------------- 7.6/21.7 MB 9.4 MB/s eta 0:00:02
       ----------------- ---------------------- 9.7/21.7 MB 9.6 MB/s eta 0:00:02
       ---------------------- ----------------- 12.3/21.7 MB 9.9 MB/s eta 0:00:01
       -------------------------- ------------- 14.4/21.7 MB 10.0 MB/s eta 0:00:01
       ------------------------------- -------- 17.0/21.7 MB 10.2 MB/s eta 0:00:01
       ----------------------------------- ---- 19.4/21.7 MB 10.4 MB/s eta 0:00:01
       ---------------------------------------  21.5/21.7 MB 10.5 MB/s eta 0:00:01
       ---------------------------------------- 21.7/21.7 MB 10.0 MB/s eta 0:00:00
    Installing collected packages: rdkit
      Attempting uninstall: rdkit
        Found existing installation: rdkit 2023.9.3
        Uninstalling rdkit-2023.9.3:
          Successfully uninstalled rdkit-2023.9.3
    Successfully installed rdkit-2024.3.5
    

      WARNING: Failed to remove contents in a temporary directory 'C:\Users\tiago\AppData\Local\Programs\Anaconda\Lib\site-packages\~dkit'.
      You can safely remove it manually.
    


```python

```


```python
import numpy as np
from rdkit import Chem
from rdkit.Chem import AllChem
from rdkit.Chem import DataStructs
from rdkit.Chem.AtomPairs import Pairs
smiles = 'FC(F)(C(F)(C(O)=O)F)C(F)(F)F'

```


```python
for atom in molecule.GetAtoms():
    prop = atom.GetProp('_GasteigerCharge')
    print('%s | %s' % (atom.GetSymbol(), prop))

```

    F | -0.18847445561314791
    C | 0.41381329177535614
    F | -0.18847445561314791
    C | 0.41320669293153911
    F | -0.18611676986581191
    C | 0.38122831825651354
    O | -0.47662566423596492
    O | -0.24490878935347329
    F | -0.18611676986581191
    C | 0.46009468700965073
    F | -0.16471144158182188
    F | -0.16471144158182188
    F | -0.16471144158182188
    


```python
fingerprint_one = AllChem.GetMorganFingerprintAsBitVect(
    molecule, 
    1,  
    nBits=512,
    useFeatures=True,
)
```


```python
for atom in molecule.GetAtoms():
    atom.SetProp('_GasteigerCharge', str(0))

for atom in molecule.GetAtoms():
    prop = atom.GetProp('_GasteigerCharge')
    print ( '%s | %s' % (atom.GetSymbol(), prop))
    break
```

    F | 0
    


```python
fingerprint_two = AllChem.GetMorganFingerprintAsBitVect(
    molecule, 
    1,  
    nBits=512,
    useFeatures=True,
)

print(DataStructs.DiceSimilarity(fingerprint_one, fingerprint_two))
```

    1.0
    


```python
import numpy as np
from rdkit import Chem
from rdkit.Chem import AllChem
from rdkit.Chem import DataStructs
from rdkit.Chem.AtomPairs import Pairs
smiles = 'FC(F)(C(F)(C(O)=O)F)C(F)(F)F'

molecule = Chem.MolFromSmiles(smiles)
AllChem.ComputeGasteigerCharges(molecule)

for atom in molecule.GetAtoms():
    prop = atom.GetProp('_GasteigerCharge')
    print ( '%s | %s' % (atom.GetSymbol(), prop))

from rdkit.Chem.Draw import SimilarityMaps
contribs = [molecule.GetAtomWithIdx(i).GetDoubleProp('_GasteigerCharge') for i in range(molecule.GetNumAtoms())]
fig = SimilarityMaps.GetSimilarityMapFromWeights(molecule, contribs, colorMap='jet', contourLines=100)
```

    F | -0.18847445561314791
    C | 0.41381329177535614
    F | -0.18847445561314791
    C | 0.41320669293153911
    F | -0.18611676986581191
    C | 0.38122831825651354
    O | -0.47662566423596492
    O | -0.24490878935347329
    F | -0.18611676986581191
    C | 0.46009468700965073
    F | -0.16471144158182188
    F | -0.16471144158182188
    F | -0.16471144158182188
    


    
![png](output_8_1.png)
    



```python

```
