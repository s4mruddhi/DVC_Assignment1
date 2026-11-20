# Dataset Versioning using DVC

Assignment 1: Implement Dataset Versioning using DVC (Data Version Control)

## Structure
```
DatasetVersioning/
├── data/
│   ├── student.csv        (tracked by DVC, ignored by Git)
│   ├── student.csv.dvc    (pointer file tracked by Git)
│   └── .gitignore
├── .git/
├── .dvc/
├── .gitignore
└── README.md
dvc-storage/               (local DVC remote, sibling folder)
```

## Setup
```
pip install dvc
dvc version
```

## Steps performed
1. `git init`
2. `dvc init` -> commit "Initialize DVC"
3. Create `data/student.csv` (4 records)
4. `dvc add data/student.csv`
5. `git add . && git commit -m "Track dataset using DVC"`  -> Version 1
6. Append `5,Neha,77`, `dvc add data/student.csv`, commit "Dataset Version 2" -> Version 2
7. `git log` to view history (Version 1 -> Version 2)
8. `git checkout <commit_id>` + `dvc checkout` restores Version 1; `git checkout main` + `dvc checkout` returns to Version 2
9. `dvc remote add -d localstorage ../dvc-storage`, commit "Configure DVC remote"
10. `dvc push`
11. Delete `data/student.csv`, recover with `dvc pull` (or `dvc checkout`)

## Commands summary
| Command | Purpose |
|---|---|
| git init | Initialize Git repository |
| dvc init | Initialize DVC |
| dvc add file | Track dataset |
| dvc push | Upload dataset to remote storage |
| dvc pull | Download dataset |
| dvc checkout | Restore dataset version |
| git add . | Stage files |
| git commit | Commit changes |

See `execution_log.txt` for the full terminal output of every step.

## Note when cloning
The remote URL is relative (`../../dvc-storage`), so keep `dvc-storage/` next to `DatasetVersioning/`.
