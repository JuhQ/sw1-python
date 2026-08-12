# File Handling in Python

Data stored in variables only persists for the duration of the program's execution, but often there is a need to store data permanently so that it is also available during future executions of the program.

Permanent storage is typically handled using databases (covered in future courses) or by writing directly to a file, from which the data can later be read.

Such data can include, for example:

- game saves
- user information
- settings
- log data
- measurement data
- etc.

A file being saved/read can contain plain text or be in some binary format (images, PDFs, DOCs, etc.).

## Saving to and Reading from a Text File

Python provides simple built-in tools for handling files. Writing to a file is done as follows:

```python
with open("save.txt", "w") as file:
    file.write("Player reached level 2.")
```

In the example above, the `open` function opens a file named `save.txt` in write mode (the second parameter of the `open` function is `"w"`). If the file does not yet exist, it is created. The `with` statement ensures that the file is closed automatically, even if an error occurs while writing. The `write` method is used to write text to the file.

When using the `w` parameter, the program overwrites the previous contents of the file. If you want to add content to the file, you can use the `a` parameter (_append_):

```python
with open("save.txt", "a") as file:
    file.write("Player reached level 3.")
```

Note that unlike printing to the console (`print()`), the `write` method does not automatically add a newline character. The contents of the file will therefore be:

```txt
Player reached level 2.Player reached level 3.
```

If necessary, a newline can be added to the string using the `\n` character (_newline_):

```python
with open("save.txt", "w") as file:
    file.write("Player reached level 4.\n")
    file.write("Player reached level 5.\n")
```

Similarly, the same file can be read as follows:

```python
with open("save.txt", "r") as file:
    data = file.read()
    print(data)
```

The `r` parameter means read mode. The `read` method reads the entire contents of the file and stores it in the variable `data`, which is then printed to the console.

Other ways to read a file include the `readline` method, which reads the file one line at a time, and the `readlines` method, which reads all lines and stores them as a list.

## Data Serialization

Serialization means converting data into a format suitable for storage.

Data stored in a computer's memory cannot always be directly saved to a file. For example, Python lists, dictionaries, or other objects often need to be converted into text format before they can be stored. JSON (JavaScript Object Notation) is a common and easy-to-use format that is well suited for serializing Python data structures. Python's [json](https://docs.python.org/3/library/json.html) library provides functions for converting data structures to JSON format and back. JSON is actively used and will be covered in more detail in the next course in connection with web programming.

```python
import json

save_data = {
    "player": "Matti",
    "level": 5,
    "equipment": ["sword", "shield", "armor"]
}

with open("save.json", "w") as file:
    json.dump(save_data, file)
with open("save.json", "r") as file:
    data_read = json.load(file)
print(f"Player: {data_read['player']}, level: {data_read['level']}, equipment: {data_read['equipment']}")
```

In the example above, a Python dictionary `data` is created containing the player's name, level, and equipment. The `json.dump` function writes this dictionary to the file `save.json` in JSON format. The file is read using the `json.load` function, which converts the contents of the JSON file back into a Python data structure.

In addition to text format, data can also be stored in binary format, which is often more efficient and faster, but requires special tools for reading and writing. The [Pickle](https://docs.python.org/3/library/pickle.html) library is one way to serialize Python objects into binary format, but in this course we focus on text-based serialization, which is also easier for humans to read and understand.

## Deleting a File

A file can be deleted using the `remove` function of Python's `os` library:

```python
import os
if os.path.exists("save.txt"):
    os.remove("save.txt")
else:
    print("File not found.")
```

In the example above, the `if` statement ensures that the file exists before it is deleted, in order to avoid an error situation.

## Error Handling

File handling can also involve various other error situations, such as read and write errors or insufficient permissions. The `try-except` structure can be used to handle different types of errors:

```python
try:
    with open("save.txt", "r") as file:
        data = file.read()
except FileNotFoundError:
    print("File not found.")
except IOError:
    print("Error occurred while handling the file.")
```

In the example above, the program attempts to open and read the file inside the `try` block. If the file is not found, the `FileNotFoundError` exception is handled and a message is printed. If another I/O error occurs, it is handled using the `IOError` exception.

Error handling can also be used in other situations where potential errors occur during program execution, even if the code itself has been written correctly. For example, information entered by the user that is not in the expected format can cause an error that can be handled using a `try-except` structure:

```python
try:
    player_age = int(input("Enter player's age: "))
except ValueError:
    print("Error: entered value is not an integer.")
print("Program execution continues.")
```

The code inside the `try` block is executed until an error occurs. When an error occurs, execution immediately jumps to the appropriate `except` block. If no error occurs, the `except` block(s) are skipped and program execution continues normally afterward.

To successfully read the player's age before continuing the program, a `while` loop can be used that repeats until the age has been read successfully:

```python
while True:
    try:
        player_age = int(input("Enter player's age: "))
        break  # age read successfully, exit the loop
    except ValueError:
        print("Error: entered value is not an integer. Please try again.")
print(f"Player's age is {player_age}.")
```

In situations where program execution could potentially fail due to a runtime error unrelated to the actual code, it is important to use error handling. Otherwise, the program will crash and its execution will end completely at that point.

---

<!-- add mermaid support for gh pages -->
<script type="module">
    Array.from(document.getElementsByClassName("language-mermaid")).forEach(element => {
      element.classList.add("mermaid");
    });
    import mermaid from 'https://cdn.jsdelivr.net/npm/mermaid@11/dist/mermaid.esm.min.mjs';
    mermaid.initialize({ startOnLoad: true });
</script>
