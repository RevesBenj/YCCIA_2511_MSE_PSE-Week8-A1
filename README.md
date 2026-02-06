# Factory Design Pattern – Simple Explanation 

## What this code doing
This program take a **name input** from user.
User can type name in **two style**:
- `First Last` (space)
- `Last, First` (comma)

System will **auto choose** correct class to split the name.
This auto choosing part is called **Factory Design Pattern**.

---

## What is Factory Pattern
Factory pattern mean:
👉 **One place decide what object to create**, not client.

Client no need to know:
- which class
- how object created

Client just ask:
> “Give me correct object”

---

## Parts of Factory Pattern in the code

### 1) Base class (Product)
```python
class Namer():
    def __init__(self):
        self.first = ""
        self.last = ""

```

- This is parent / base

- All name parser follow this structure


### 2) Concrete Classes (Actual Objects)
### FirstFirst class

```python
class FirstFirst(Namer):
    def __init__(self, namestring):
        super().__init__()
        names = namestring.split(" ")
        self.first = names[0]
        self.last = names[1]

```

 - Used when input is First Last

 - Split by space

### LastFirst class

```python
class LastFirst(Namer):
    def __init__(self, namestring):
        super().__init__()
        names = namestring.split(",")
        self.last = names[0]
        self.first = names[1]

```
- Used when input is Last, First

- Split by comma

###3) Factory Class (Main Factory Logic)

```python
class NamerFactory():
    def __init__(self, namestring):
        self.name = namestring

    def getNamer(self):
        if "," in self.name:
            return LastFirst(self.name)
        else:
            return FirstFirst(self.name)

```

- This is the Factory

- It checks input at runtime

- Decide which class to create

- Return correct object

- Client never create FirstFirst or LastFirst directly.

## How Client Use the Factory


```python
factory = NamerFactory(name)
namer = factory.getNamer()

print(namer.first, namer.last)

```

- Client only talk to factory

- Client use result same way every time

- Client don’t care about class type

## Output / Result When Program Run

### Example

| User Input     | Output       |
|----------------|--------------|
| Benj Patiag     | Benj Patiag   |
| Patiag, Benj    | Benj Patiag   |

### Same behavior for
- Console program
- GUI (Tkinter window)


## Why This is Factory Pattern

- Object creation is separate from client

- Code is clean and flexible

- Easy to add new name format later


---

# Factory Design Pattern per file:

## NameUi_with_factory_comments.py
This file build a simple **GUI window** where user type a name and click Compute to split first and last name.  
Factory Design Pattern is used by `NamerFactory`, which decide at runtime whether to create `FirstFirst` or `LastFirst` based on comma in the input.  
GUI code never create the parser class directly; it only ask the factory and use the returned object.


## NamerConsole_with_factory_comments.py
This file run in **console mode** and keep asking user to enter a name until `quit` is typed.  
Factory Design Pattern is applied the same way, where `NamerFactory` choose the correct name parser class automatically.  
Console code stay simple because object creation logic is hidden inside the factory.


## Cocoon_with_factory_comments.py
This file show another simple example of Factory Pattern using a `Cocoon` class.  
The factory method `getButterfly()` decide which `Butterfly` subclass to create based on the value of `y`.  
Client code do not know which butterfly type it get, only that it receive a `Butterfly` object.
