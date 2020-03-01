## Typescript Basics

### Variables

#### Basic variable types
```typescript
let anyVar: any = 'string';
let stringVar: string = 'string';
let numVar: number = 100;
let booleanVar: boolean = true;
let voidVar: void = undefined;
let nullVar: null = null;
let undefinedVar: undefined = undefined;
```

### Structures

#### Define what types are expected in an array
```typescript
let stringArray: Array<string> = ['one', 'two', 'three'];
let numberArray: Array<number> = [1,2,3];
let booleanArray: Array<boolean> = [true, false];
```

#### Tuples are arrays expecting certain types at certain positions
```typescript
let tupleArray: [string, number, boolean] = ['one', 2, true];
```

## Functions

+ Function arguments and return type can be defined.
+ Return type is defined after the arguments ()

```typescript
function add(x: number, y: number): number {
    return x + y;
}
```

Add ? after argument to set it as optional
```typescript
function hello(name?: string): string {
    return `Hello ${name ? name : 'World'}`; 
}
```

Function with object with defined interface as argument
```typescript
function editPost(post: {id: number, title: string, content: string}) {
    // ...function body
}
```

Separate interface definition for an object
```typescript
interface Post {
    id: number,
    title: string,
    content: string,
};

function createPost(newPost: Post): Post {
    return newPost;
}
```

### Classes

+ Can define access controls on class properties / methods
+ Public (default) = property can be accessed from outside class definition - e.g userOne.id
+ Private = property can only be accessed from inside class definition
+ Protected = property can be accessed within definitions of other classes which extend this class
+ Readonly = property is read only - can not be set to a different value. These need to be initialised when declared, or in the constructor
+ Static = properties on the class rather than instances of the class - accessed using User.property rather than this.property

#### Accessors
+ Can define getters and setters to access/update private properties - this allows putting rules in place, e.g validation, when changing values on an instance

```typescript
class User {
    _id: number;
    private _name: string;
    private _email: string;
    private _password: string;

    constructor(id: number, name: string, email: string, password: string) {
        this._id = id;
        this._name = name;
        this._email = email;
        this._password = password;
    }

    get name(): string {
        return this._name;
    }

    set name(name: string) {
        if(name.length >= 255) {
            throw new Error('Name is too long');
        }
    }
}
```

### Abstract Classes

+ Abstract classes can not be instantiated directly, they provide base structure for other classes to extend
+ Any methods marked as abstract within an abstract class does not define implementation - it just says this method should exist on extended classes
+ The implementaion must be defined when creating extended classes

```typescript
abstract class Page {
    heading: string;

    constructor(heading: string){
        this.heading = heading;
    }

    abstract generateMetaTitle()
}
```

Extending the abstract class from above - here we define the implementation of the abstract method generateMetaTitle()

```typescript
class ArticlePage extends Page {
    constructor(heading: string){
        super(heading);
    }

    generateMetaTitle(): string {
        return `${this.heading} | My Blog Site`;
    }
}
```