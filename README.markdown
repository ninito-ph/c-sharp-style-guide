# ninito-ph C# Style Guide

## **PLEASE, REFER TO MY [NEW, MORE COMPREHENSIVE AND UP-TO-DATE UNITY STYLE GUIDE](https://github.com/ninito-ph/Unity-Style-Guide). THIS GUIDE HERE IS BEING LEFT FOR ARCHIVAL PURPOSES.**



This style guide is a fork of raywenderlich's C# style guide.  

Its overarching goals are **conciseness**, **readability** and **simplicity**. Also, this guide is written primarily for **Unity**. 

## Inspiration

This style guide is based on C# and Unity conventions. 

## Table of Contents

- [Comments and Documentation](#comments--documentation)  
- [Nomenclature](#nomenclature)
  + [Namespaces](#namespaces)
  + [Classes & Interfaces](#classes--interfaces)
  + [Methods](#methods)
  + [Fields](#fields)
  + [Parameters](#parameters--parameters)
  + [Delegates](#delegates--delegates)
  + [Events](#events--events)
  + [Misc](#misc)
- [Declarations](#declarations)
  + [Access Level Modifiers](#access-level-modifiers)
  + [Fields & Variables](#fields--variables)
  + [Classes](#classes)
  + [Interfaces](#interfaces)
  + [Attributes](#attributes)
- [Spacing](#spacing)
  + [Indentation](#indentation)
  + [Line Length](#line-length)
  + [Vertical Spacing](#vertical-spacing)
- [Regions](#regions)
- [Brace Style](#brace-style)
- [Switch Statements](#switch-statements)
- [Language](#language)
- [Credit](#credits)


## Comments and Documentation

All methods and classes should have names that makes their purpose evident. To further aid in making code as easily comprehensible as possible, every method and class should be documented in XML (except for Unity callbacks), and particularly complex sections should be documented with regular comments, in a step-by-step style.

**AVOID**:

```csharp
public override void OnGUI(Rect position, SerializedProperty property, GUIContent label)
```

**PREFER**:

```csharp
/// <summary>
///   <para>Override this method to make your own IMGUI based GUI for the property.</para>
/// </summary>
/// <param name="position">Rectangle on the screen to use for the property GUI.</param>
/// <param name="property">The SerializedProperty to make the custom GUI for.</param>
/// <param name="label">The label of this property.</param>
public override void OnGUI(Rect position, SerializedProperty property, GUIContent label)
```

## Nomenclature

On the whole, naming should follow C# standards.

### Namespaces

Namespaces are all **PascalCase**, multiple words concatenated together, without hyphens ( - ) or underscores ( \_ ). The exception to this rule are acronyms like GUI or HUD, which can be uppercase:

**AVOID**:

```csharp
com.raywenderlich.fpsgame.hud.healthbar
```

**PREFER**:

```csharp
RayWenderlich.FPSGame.HUD.Healthbar
```

### Classes & Interfaces

Classes and interfaces are written in **PascalCase**. For example `RadialSlider`. 

### Methods

Methods are written in **PascalCase**. For example `DoSomething()`. 

### Fields

All non-static fields are written **camelCase**. Per Unity convention, this includes **public fields** as well.

For example:

```csharp
public class MyClass 
{
    public int publicField;
    int packagePrivate;
    private int myPrivate;
    protected int myProtected;
}
```

**AVOID:**

```csharp
private int _myPrivateVariable
```

**PREFER:**

```csharp
private int myPrivateVariable
```

Static fields are the exception and should be written in **PascalCase**:

```csharp
public static int TheAnswer = 42;
```
### Properties

All properties are written in **PascalCase**. For example:

```csharp
public int PageNumber 
{
    get { return pageNumber; }
    set { pageNumber = value; }
}
```

### Parameters

Parameters are written in **camelCase**.

**AVOID:**

```csharp
void DoSomething(Vector3 Location)
```

**PREFER:**

```csharp
void DoSomething(Vector3 location)
```

Single character values are to be avoided except for temporary looping variables.

### Actions

Actions are written in **PascalCase**. For example:

```csharp
public event Action<int> ValueChanged;
```

### Misc

In code, acronyms should be treated as words. For example:

**AVOID:**

```csharp
XMLHTTPRequest
String URL
findPostByID
```  

**PREFER:**

```csharp
XmlHttpRequest
String url
findPostById
```

## Declarations

### Access Level Modifiers

Access level modifiers should be explicitly defined for classes, methods and member variables.

### Fields & Variables

Prefer single declaration per line.

**AVOID:**

```csharp
string username, twitterHandle;
```

**PREFER:**

```csharp
string username;
string twitterHandle;
```

### Classes

Exactly one class per source file, although inner classes are encouraged where scoping appropriate.

### Interfaces

All interfaces should be prefaced with the letter **I**. 

**AVOID:**

```csharp
RadialSlider
```

**PREFER:**

```csharp
IRadialSlider
```

### Attributes

All attributes should be placed on their own line, directly above whatever they're modifying.

**AVOID:**

```csharp
[SerializeField] [Tooltip("Many attributes on a single line!")] [Range(0, 1)]
private int variable;
```

**PREFER:**

```csharp
[SerializeField]
[Tooltip("Many attributes stacked!)]
[Range(0, 1)]
private int variable;
```

## Spacing

Spacing is especially important in code, as it needs to be easily readable at any point. 

### Indentation

Indentation should be done using **tabs**, never spaces.  

#### Blocks

Indentation for blocks uses **one tab, configured as 4-spaces long (Default in most IDEs)** for optimal readability:

**AVOID:**

```csharp
for (int i = 0; i < 10; i++) 
{
    Debug.Log("index=" + i);
}
```

**PREFER:**

```csharp
for (int i = 0; i < 10; i++) 
{
    Debug.Log("index=" + i);
}
```

#### Line Wraps

Indentation for line wraps should use **2 tabs** (not the default 1):

**AVOID:**

```csharp
CoolUiWidget widget =
    someIncrediblyLongExpression(that, reallyWouldNotFit, on, aSingle, line);
```

**PREFER:**

```csharp
CoolUiWidget widget =
        someIncrediblyLongExpression(that, reallyWouldNotFit, on, aSingle, line);
```

### Line Length

Lines should be no longer than **120** characters long.

### Vertical Spacing

There should be exactly one blank line between methods to aid in visual clarity 
and organization. Whitespace within methods should separate functionality, but 
having too many sections in a method often means you should refactor into
several methods.

Furthermore, there should always be one blank line between #region and #endregion
declarations before methods or members contained in said region.

## Regions

All code contained within a class or struct should be separated into regions. Regions should be separated and ordered as follows:

- Fields
  - Private Fields (Private members with SerializeField attribute always come first)
  - Protected Fields
  - Public Fields
- Properties
- Methods
  - Unity Callbacks
  - Abstract Implementations
  - Interface Implementations (One separate region for each interface, e.g. #region IInterface Implementation, #IOtherInterface Implementation, etc.)
  - Private Methods
  - Protected Methods
  - Public Methods
- Inner Classes/Structs (One separate region for each class, e.g. #region NestedClass Class, #region OtherNestedClass Class, etc.)

**AVOID:**

```csharp
class MyClass
{
    public bool myBool; 
    private int myInt;
    protected float myFloat;

    private void DoStuff()
    {
        if (someCondition)
        {
          // ...
        }
        else
        {
          // ...
        }
    }
    
    private void Start()
    {
        // ...
    }
}
```

**PREFER:**

```csharp
class MyClass
{
    #region Private Fields
    
    private int myInt;
    
    #endregion
    
    #region Protected Fields
    
    protected float myFloat;
    
    #endregion
    
    #region Public Fields
    
    public bool myBool; 
    
    #endregion

    #region Unity Callbacks
    
    private void Start()
    {
        // ...
    }
    
    #endregion
    
    #region ISerializationCallbackReceiver Implementation
    
    private void OnBeforeSerialize()
    {
        // ...
    }
    
    #endregion

    #region Private Methods

    private void DoStuff()
    {
        if (someCondition)
        {
          // ...
        }
        else
        {
          // ...
        }
    }
    
    #endregion
}
```

## Brace Style

All braces get their own line as it is a C# convention:

**AVOID:**

```csharp
class MyClass {
    void DoSomething() {
        if (someTest) {
          // ...
        } else {
          // ...
        }
    }
}
```

**PREFER:**

```csharp
class MyClass
{
    void DoSomething()
    {
        if (someTest)
        {
          // ...
        }
        else
        {
          // ...
        }
    }
}
```

Conditional statements are always required to be enclosed with braces,
unless it is a single call that does not require wrapping.

**AVOID:**

```csharp
if (someTest)
    doSomething();

if (someTest) 
{
  return;
}
```

**PREFER:**

```csharp
if (someTest) 
{
    DoSomething();
    DoSomethingElse();
}  

if (someTest) return;
```
## Switch Statements

Switch-statements come with `default` case by default. If the `default` case is never reached, be sure to remove it.

**AVOID:**  
  
```csharp
switch (variable) 
{
    case 1:
        break;
    case 2:
        break;
    default:
        break;
}
```

**PREFER:**  
  
```csharp
switch (variable) 
{
    case 1:
        break;
    case 2:
        break;
}
```

## Language

Use US English spelling for class, method and variable names, as well as documentation.

**AVOID:**

```csharp
string colour = "red";
```

**PREFER:**

```csharp
string color = "red";
```

The exception here is `MonoBehaviour` as that's what the class is actually called.


## Credits:

This style is a fork of raywenderlich's C# style guide.

- [raywenderlich.com](https://github.com/raywenderlich/c-sharp-style-guide)
