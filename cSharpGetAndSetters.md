
## CSharp

#### Set up a Namespace and Class
```csharp
namespace NameOfNamespace
{
  attribute class NameOfClass
  {

  }
}
```
Example
```csharp
namespace MyProject
{
  public class Project
  {
    //Everything goes here  
  }
}

```


#### How to create a property inside a class

```csharp

attributes _propertyName;
```
Example
```csharp
private string _input1;

//properteis should always have the attribute private

```

#### How to create a Setter inside a class

```csharp
attributes NameOftheFunction( attribute prameter)
{
 _property = parameter;
}
```
Example
```csharp
public void SetInput1 (string aString)
{
  _input1 = aString;
}
//Attribute examples are: public, private, void, string, int, static
```
#### How to write a Getter inside a class

```csharp
attributes AnyName ()
{
  return _property
}
```
Example
```csharp
 public string GetInput1 ()
 {
   return _input1
 }
```

#### How to create an instance of a class

```csharp

ClassName newIstanceName = new ClassName ();
//Attribute examples are: public, private, void, string, int, static
```
Example
```csharp
Project newProject = new Project ();
```

#### How to use a method in a class on an instance of the class

```csharp

newIstanceName.MethodName(parameters?);
//Attribute examples are: public, private, void, string, int, static
```
Example
```csharp
newProject.SetInput1("hello");
```


