# File I/O Practice

### Objective

Practice basic Linux file input/output operations using fundamental commands.

---

## 1. Create a File

### Command

```bash
touch notes.txt
```
- Creates an empty file named `notes.txt`.

---

## 2. Write the First Line

### Command

```bash
echo "Linux file I/O practice" > notes.txt
```
- Writes the text to the file. 

---

## 3. Append the Second Line

### Command

```bash
echo "Learning Linux commands" >> notes.txt
```
- Adds the text to the end of the file without removing existing content.

---

## 4. Append the Third Line Using tee

### Command

```bash
echo "Practicing DevOps fundamentals" | tee -a notes.txt
```

### Output

```text
Practicing DevOps fundamentals
```
- Displays the text on the terminal and appends it to notes.txt.

---

## 5. Read the Entire File

### Command

```
cat notes.txt
```

### Output

```
Linux file I/O practice
Learning Linux commands
Practicing DevOps fundamentals
```
- Displays the complete contents of the file.

---

## 6. Read the First Two Lines

### Command

```bash
head -n 2 notes.txt
```

### Output

```
Linux file I/O practice
Learning Linux commands
```
- Displays only the first two lines of the file.

---

## 7. Read the Last Two Lines

### Command

```bash
tail -n 2 notes.txt
```

### Output

```
Learning Linux commands
Practicing DevOps fundamentals
```
- Displays only the last two lines of the file.

---

# Key Learnings

- `touch` creates a new empty file.
- `>` writes data and overwrites existing content.
- `>>` appends data without deleting existing content.
- `tee -a` writes to a file and displays the output simultaneously.
- `cat` reads the entire file.
- `head` displays the beginning of a file.
- `tail` displays the end of a file.
