[6 ECMAScript Data Types and Values](https://tc39.github.io/ecma262/#sec-ecmascript-data-types-and-values)

* [6.1 ECMAScript Language Types](https://tc39.github.io/ecma262/#sec-ecmascript-language-types)  
* [6.2 ECMAScript Specification Types](https://tc39.github.io/ecma262/#sec-ecmascript-specification-types)  

## [6.1 ECMAScript Language Types](https://tc39.github.io/ecma262/#sec-ecmascript-language-types)

An *ECMAScript language type* corresponds to values that are directly manipulated by an ECMAScript programmer using the ECMAScript language.  
The ECMAScript language types are `Undefined`, `Null`, `Boolean`, `String`, `Symbol`, `Number`, and `Object`.  
An *ECMAScript language value* is a value that is **characterized** by an ECMAScript language type.

### [6.1.1 The Undefined Type](https://tc39.github.io/ecma262/#sec-ecmascript-language-types-undefined-type)

The Undefined type has exactly one value, called **undefined**.  
Any variable that <u>has not been assigned</u> a value has the value undefined.

### [6.1.2 The Null Type](https://tc39.github.io/ecma262/#sec-ecmascript-language-types-null-type)

The Null type has exactly one value, called **null**.

### [6.1.3 The Boolean Type](https://tc39.github.io/ecma262/#sec-ecmascript-language-types-boolean-type)

The Boolean type represents a logical entity having two values, called **true** and **false**.

### [6.1.4 The String Type](https://tc39.github.io/ecma262/#sec-ecmascript-language-types-string-type)

The String type is the set of all *ordered sequences* of zero or more 16-bit unsigned integer values (“elements”) up to a maximum length of 2<sup>53</sup> - 1 elements.

The String type is generally used to represent **textual** data in a running ECMAScript program, in which case each element in the String is treated as a UTF-16 code unit value.

Each element is regarded as occupying a **position** within the sequence. These positions are indexed with nonnegative integers. The first element (if any) is at index 0, the next element (if any) at index 1, and so on.

The **length** of a String is the number of elements (i.e., 16-bit values) within it. The empty String has length zero and therefore contains no elements.

### [6.1.5 The Symbol Type](https://tc39.github.io/ecma262/#sec-ecmascript-language-types-symbol-type)

The Symbol type is the set of all non-String values that may be used as the key of an Object property (6.1.7).

Each possible Symbol value is unique and immutable.

Each Symbol value immutably holds an associated value called [[Description]] that is either **undefined** or a **String** value.

#### [6.1.5.1 Well-Known Symbols](https://tc39.github.io/ecma262/#sec-well-known-symbols)

Well-known symbols are built-in Symbol values that are explicitly referenced by algorithms of this specification.  
They are typically used as *the keys of properties* whose values serve as extension points of a specification algorithm.  
Unless otherwise specified, well-known symbols values are **shared** by all realms.

### [6.1.6 The Number Type](https://tc39.github.io/ecma262/#sec-ecmascript-language-types-number-type)

The Number type has exactly 18437736874454810627 (that is, 2<sup>64</sup> - 2<sup>53</sup> + 3) values, representing the double-precision 64-bit format IEEE 754-2008 values as specified in the IEEE Standard for Binary Floating-Point Arithmetic, except that the 9007199254740990 (that is, 2<sup>53</sup> - 2) distinct “Not-a-Number” values of the IEEE Standard are represented in ECMAScript as a single special **NaN** value. (Note that the NaN value is produced by the program expression NaN.)  
In some implementations, external code might be able to detect a difference between various Not-a-Number values, but such behaviour is implementation-dependent; to ECMAScript code, all NaN values are indistinguishable from each other.

### [6.1.7 The Object Type](https://tc39.github.io/ecma262/#sec-object-type)

An Object is logically a **collection** of properties. Each property is either a *data* property, or an *accessor* property:

* A *data property* associates a key value with an [ECMAScript language value](https://tc39.github.io/ecma262/#sec-ecmascript-language-types) and a set of Boolean attributes.  
* An *accessor property* associates a key value with one or two accessor functions, and a set of Boolean attributes. The accessor functions are used to store or retrieve an [ECMAScript language value](https://tc39.github.io/ecma262/#sec-ecmascript-language-types) that is associated with the property.  

Properties are identified using *key values*. A property key value is either an ECMAScript String value or a Symbol value. All String and Symbol values, including the empty string, are valid as property keys. A property name is a property key that is a String value.

Property keys are used to access properties and their values. There are two kinds of access for properties: *get* and *set*, corresponding to value **retrieval** and **assignment**, respectively.  
The properties accessible via get and set access includes both *own properties* that are a direct part of an object and *inherited properties* which are provided by another associated object via a property inheritance relationship. Inherited properties may be either own or inherited properties of the associated object. Each own property of an object must each have a key value that is distinct from the key values of the other own properties of that object.

<u>All objects are logically **collections** of *properties*</u>, but there are multiple forms of objects that differ in their semantics for accessing and manipulating their properties. *Ordinary objects* are the most common form of objects and have the default object semantics. An *exotic object* is any form of object whose property semantics differ in any way from the default semantics.

---

* [6.1.7.1 Property Attributes](https://tc39.github.io/ecma262/#sec-property-attributes)  
* [6.1.7.2 Object Internal Methods and Internal Slots](https://tc39.github.io/ecma262/#sec-object-internal-methods-and-internal-slots)  
* [6.1.7.3 Invariants of the Essential Internal Methods](https://tc39.github.io/ecma262/#sec-invariants-of-the-essential-internal-methods)  
* [6.1.7.4 Well-Known Intrinsic Objects](https://tc39.github.io/ecma262/#sec-well-known-intrinsic-objects)  

## [6.2 ECMAScript Specification Types](https://tc39.github.io/ecma262/#sec-ecmascript-specification-types)
