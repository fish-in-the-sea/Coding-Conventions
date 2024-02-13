----
# Microsoft C# conventions
### Naming
- Public fields and constants should use PascalCase
- Private members and local values should use camelCase
	- Private fields should also begin with a `_`
```c#
public int PublicInt;
private int _privateInt;
```

- Arguments should be written in camelCase
```c#
public int Damage(int damageAmount, AttackTypes damageType);
```

- Static fields should start with `s_`
```c#
public static int s_Field;
```

- For enums use singular nouns.
	- except for when the enum is a flag then it should be plural
```c#
pubic enum Suit 
{
	Spades,
	Clubs,
	Diamonds,
	Hearts
}
//can only be one

[Flags]
pubic enum AttackTypes
{
	Elemental,
	Poison,
	Physical,
}
//can pick multiple
```

- Interfaces should begin with an `I` 
```c#   
interface IEquipable
{
	...
}
```

- Attributes end with the word `Attribute` 
```c#   
public class CustomAttribute : Attribute
{
	...
}
[CustomAttribute]
public void Foo();
```

- Type parameters should either be `T` or start with `T`
```c#
public List<T> Inventory;
//or
public List<TEquipment> Inventory;
```

-----

### Code Styling
- Use modern C# whenever possible
- Use LINQ for better readability
```c#
//// Filtering
> int[] numbers = {1, 2, 3, 4, 5, 7, 8, 9};
> var filteredNumbers = numbers.Where(x => x > 5);
> foreach(var num in filteredNumbers)
> {
> 	Console.Writeline(num);
> }
6
7
8
//// Projetion (mapping)
> int[] numbers = {1, 2, 3, 4, 5, 7, 8, 9};
> var squaredNumbers = numbers.Select(x => x * x);
> foreach(var num in squaredNumbers)
> {
> 	Console.Writeline(num);
> }
1
4
9
...
//// Sorting
> int[] numbers = {5, 2, 1, 4, 3, 8, 7, 9};
> var squaredNumbers = numbers.OrderBy(x => x);
> foreach(var num in squaredNumbers)
> {
> 	Console.Writeline(num);
> }
1
2
3
...
```
- LINQ also supports a querying
```c#
var criticalEnemies = from entity in entities
					  where entity.type == EntityType.Enemy
					  where entity.GetHealth < 5
					  select entity;
```

- Use data types over runtime types `string` vs `System.String`
- When building strings, use string interpolation
```c#
string status = $"Health: {Player.GetHealth()}, Stamina: {Player.GetStamina()}";
// for constructing large strings use System.Text.StringBuilder
```

- When initializing arrays use concise syntax
```c#
string[] vowels = {"a", "e", "i", "o", "u"};
// or
var vowels = new string[] {"a", "e", "i", "o", "u"};
```

- Delegates should use `Func< >` and `Action< >` for defining types.
```c#
Action<int> Heal = (amount) => ...;
Action<int, AttackTypes> Attack = (damage,damageType) => ...;
Func<int> GetHealth = () => Player.GetHealth;

Heal(12);
Attack(10, AttackTypes.Physical | AttackTypes.Elemental);
GetHealth();
```

- Use lambdas to subscribe to event handlers that do not need to be removed.
```c#
// Good practice. 
public Box()
{
	this.Collision += (Entity) => Console.Writeline(Entity);
}


// Bad practice.
public Box()
{
	this.Collision += new EventHandler(CollisionLogger);
}

void CollisionLogger(Entity)
{
	Console.Writeline(Entity);
}
```

- Use implicit typing for looping
```c#
for(var i = 0; i < 1000; i++) ...
// or 
foreach(var i in arr) ...
```

-------
## Styling Guides
- Use four spaces not tabs
- Align code consistently
- Limit lines to 65 characters
- Break long statements into multiple lines with current indentation braces line up with current indentation level.
	- Line breaks should occur before binary operators if necessary
- Avoid usage of `var` unless the type is easy to infer
```c#
// good
var number = 1.2f;
var str    = "hello";

// bad
var unknown = foo();
var status = Player.Status();
```

 - Use concise format for class instantiation.
```c#
var player = new Player();
Player player = new();
Player player = new Player();
// All these methods are equivilent
```
-----
## Comment style
- Using single line comments `//` for brief explanations
- Avoid multi-line comments `/* */` for longer explanations.
- For describing methods, classes, fields, and public members use XML comments
```c#
/// <sumary>
/// This is a class.
/// </sumary>
public class MyClass { }


/** 
* <summary>
* Handles an entity taking damage.
* </summary>
* <param name="damage">Amount of damage dealt as int. </param>
* <param name="damageTypes"> Damage Types dealt as a AttackTypes enum. </param>
* <returns> Remaing health of entity </returns>
*/
public int Damage(int damage, AttackTypes damageTypes);
```
- Comments on the next line, not at the end
- Use complete sentences, end in a `.`
- Pad the beginning of a comment with a `' '`

-----

## Layout
- Four spaces not tabs
- One Statement per line
- One Declaration per line
- Add at least one blank line between method definitions and property definitions
- Use parentheses to make clauses in an expression apparent
```c#
if ((health < 10) && !Dead) ...
```