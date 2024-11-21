# Code Documentation: `bulk_rename` Function

## Purpose:
The `bulk_rename` function renames files in a specified folder, either preserving their original names and appending numbers or replacing their names entirely with sequential numbers.

---

## Function Definition:
```python
def bulk_rename(folder_path, keep_original_name=True):
```
- **Parameters**:
  - `folder_path` (str): Path to the folder containing the files to be renamed.
  - `keep_original_name` (bool): If `True`, the original file names are preserved with a sequential number appended. If `False`, the files are renamed to sequential numbers only.

---

## Key Steps in the Function:

### 1. **Retrieve Files**:
```python
files = os.listdir(folder_path)
```
- Uses `os.listdir` to get a list of all files and directories in the folder specified by `folder_path`.
- Note: The list includes both files and directories; this function assumes the folder contains only files.

---

### 2. **Sort Files**:
```python
files.sort()
```
- Sorts the file names alphabetically to ensure renaming happens in a predictable order.

---

### 3. **Rename Files**:
The function loops through each file, determines the new name, and renames it.

#### Extract File Extension:
```python
_, ext = os.path.splitext(filename)
```
- Splits the filename into its name (`_`) and extension (`ext`).

#### Generate New File Name:
- If `keep_original_name` is `True`:
  ```python
  name, _ = os.path.splitext(filename)
  new_filename = f"{name} {i}{ext}"
  ```
  - Retains the original file name and appends a sequential number (`i`) before the file extension.
  
- If `keep_original_name` is `False`:
  ```python
  new_filename = f"{i}{ext}"
  ```
  - Replaces the original file name with the sequential number (`i`) while retaining the file extension.

#### Rename File:
```python
os.rename(os.path.join(folder_path, filename), os.path.join(folder_path, new_filename))
```
- Renames the file using `os.rename` by providing the full paths of the old and new file names.

#### Print Status:
```python
print(f"Renamed {filename} to {new_filename}")
```
- Outputs the renaming operation for user feedback.

---

## Example Usage:
### Input:
Folder contents before running the function:
```
photo1.jpg
photo2.jpg
document.pdf
```

### Run:
```python
bulk_rename("C:/example_folder", keep_original_name=False)
```

### Output:
Folder contents after execution:
```
1.jpg
2.jpg
3.pdf
```

---

## Notes:
- **Error Handling**: The function does not currently handle errors like invalid paths, permission issues, or non-file entries in the directory. Adding error handling could improve robustness.
- **Assumptions**: Assumes all entries in the directory are files. Directories or non-standard entries (e.g., symbolic links) may cause errors.
