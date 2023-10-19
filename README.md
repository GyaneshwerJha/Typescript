## Typescript

**Interfaces and Types**

```typescript
// Definition of the Object Interface
interface Obj {
  height: number;
  weight: number;
  gender?: boolean;
}

// Definition of a Function Type
type FuncType = (n: number, m: number) => void;

// Extension of the Object Interface
interface NewObj extends Obj {
  scolar: boolean;
  func: FuncType;
}

// Creation of objects using the extended interface
const gigi: NewObj = {
  height: 3434,
  weight: 3434,
  scolar: true,
  func: (n, m) => {
    console.log(n * m);
  },
};

const kendal: NewObj = {
  height: 43434,
  scolar: true,
  weight: 545,
  func: (n, m) => {
    console.log(n * m);
  },
}

// Calling a function from the object
kendal.func(20, 10);

// Objects with the base interface
const obj: Obj = {
  gender: true,
  height: 3434,
  weight: 34,
};

const obj2: Obj = {
  gender: false,
  height: 4434,
  weight: 94,
};

const obj3: Obj = {
  height: 4434,
  weight: 94,
};
```
**Function Definitions**

```typescript
// Function type with optional parameter
type FuncType = (n: number, m: number, l?: number) => number;

// Optional Parameter
const func: FuncType = (n, m, l) => {
  if (typeof l === "undefined") return n * m;
  return n * m * l;
};

func(25, 23);

// Default Parameter
const func: FuncType = (n, m, l = 20) => {
  return n * m * l;
};

func(25, 23);

// Rest Operator
type FuncType = (...m: number[]) => number[];
const func: FuncType = (...m) => {
  return m;
};
func(25, 23, 34, 6, 67, 8, 9);


function lol(n: number): number {
  return 45;
}
```

**Function with Object**

```typescript
// Definition of the Product Interface
interface Product {
  name: string;
  stock: number;
  price: number;
  photo: string;
  readonly id: string;
}

// Type for a function that accepts Product
type GetDataType = (product: Product) => void;

// Function to log data of a product
const getData: GetDataType = (product) => {
  console.log(product);
};

// Creating a product object
const productOne: Product = {
  name: "Macbook",
  stock: 46,
  price: 999999,
  photo: "samplephotourl",
  id: "asdnasjdasjkdas",
};

// Calling the function with the product
getData(productOne);

## Never Type

```typescript
// Function that never returns
const errorHandler = (): never => {
  throw new Error();
};
```
**Classes**

```typescript
// Class Player
class Player {
  public readonly id: string;
  constructor(private height: number, public weight: number, protected power: number) {
    this.id = String(Math.random() * 100);
  }

  get getMyHeight(): number {
    return this.height;
  }

  set changeHeight(val: number) {
    this.height = val;
  }
}

// Creating an instance of Player
const abhi = new Player(100, 150, 23);

// Accessing and modifying properties
console.log("Height", abhi.getMyHeight);
abhi.changeHeight = 500;
console.log("Height", abhi.getMyHeight);

// Class Player2 extending Player
class Player2 extends Player {
  special: boolean;
  constructor(height: number, weight: number, power: number, special: boolean) {
    super(height, weight, power);
    this.special = special;
  }
  getMyPower = () => this.power;
}

// Creating an instance of Player2
const abhi2 = new Player2(100, 150, 23, true);
console.log("Weight", abhi2.weight);
console.log("Height", abhi2.getMyHeight());
console.log("Power", abhi2.getMyPower());
```

**Interface and Generic**

```typescript
// Interface with index signature
interface Person {
  name: string;
  email: string;
}

// Accessing object properties using key
let key = "name";
const name = myobj[key as keyof typeof myobj];

// Functions to retrieve object properties
const getName = (): string => {
  return myobj["name"];
};
const getEmail = (): string => {
  return myobj["email"];
};

const getData = (key: keyof Person): string => {
  return myobj[key];
};

getData("name");
```

**Type Utility**
```typescript
// Partial<Type> - Makes properties optional
type User = {
  name: string;
  email: string;
};
type User2 = Partial<User>;

// Required<Type> - Makes all properties required
type User = {
  name?: string;
  email: string;
};
const user: Required<User> = {
  name: "abhi",
  email: "abhi@gmail.com",
};

// Readonly<Type> - Makes properties read-only
type User = {
  name: string;
  email: string;
};
const user: Readonly<User> = {
  name: "abhi",
  email: "abhi@gmail.com",
};

## Other Type Utilities (Omit, Exclude, Extract, NonNullable, Parameters, ConstructorParameters, ReturnType, InstanceType)

```typescript
// Record<Keys, Type>
type User = {
  name: string;
  email: string;
};
type User2 = Record<"name" | "email" | "gender", string>;

// Example of Record
interface UserInfo {
  age: number;
}
type UserName = "john" | "levi" | "elon" | "jack";
const users: Record<UserName, UserInfo> = {
  john: { age: 34 },
  levi: { age: 34 },
  elon: { age: 34 },
  jack: { age: 34 },
};

// Pick<Type, Keys>
interface OrderInfo {
  readonly id: string;
  user: string;
  city: string;
  state: string;
  country: string;
  status: string;
}
type ShippingInfo = Pick<OrderInfo, "city" | "state" | "country">;

// Omit<Type, Keys>
interface ShippingInfo {
  city: string;
  state: string;
  country: string;
}
type Random = Omit<ShippingInfo, "country">;

// Exclude<Type, ExcludedUnion>
type MyUnion = string | number | boolean;
type Random = Exclude<MyUnion, boolean>;

// Extract<Type, Union>
type MyUnion = string | number | boolean;
type Random = Extract<MyUnion, boolean>;

// NonNullable<Type>
type MyUnion = string | number | boolean | null | undefined;
type Random = NonNullable<MyUnion>;
type Random2 = Exclude<MyUnion, undefined | null>;

// Parameters<Type>
const myfunc = (a: number, b: string) => {
  console.log(a + b);
};
type Random = Parameters<typeof myfunc>;

// ConstructorParameters<Type>
class SampleClass {
  constructor(public s: string, public t: string) {}
}
type Random = ConstructorParameters<typeof SampleClass>;

// ReturnType<Type>
const myfunc = (a: number, b: string): string => {
  return a + b;
};
type FuncType = ReturnType<typeof myfunc>;

// InstanceType<Type>
class SampleClass {
  constructor(public s: string, public t: string) {}
}
type Random = InstanceType<typeof SampleClass>;
const user: Random = {
  s: "44",
  t: "ssds",
};
```

**Generics**

```typescript
// Generic function
const func = <T>(n: T): T => {
  return n;
};

const ans = func(20);
const ans2 = func("20");
const ans3 = func(true);

// Generic function with specified type
type Person = {
  name: string;
  age: number;
};

const func = <T>(n: T): T => {
  return n;
};

const person1: Person = {
  name: "Abhi",
  age: 109,
};

const ans = func<Person>(person1);

// Generic function with multiple type parameters
const func = <T, U>(n: T, o: U): { n: T; o: U } => {
  return { n, o };
};

const ans = func<number, string>(20, "Lol");

//Generic function with type constraint
type Person = {
  name: string;
  age: number;
};

type Person2 = {
  name: string;
  age: number;
  email: string;
};

const user: Person = {
  name: "abhi",
  age: 109,
};

const user2: Person2 = {
  name: "abhi",
  age: 109,
  email: "asd@gmail.com",
};

const func = <T, U extends T>(n: T, o: U): { n: T; o: U } => {
  return { n, o };
};

const ans = func<Person, Person2>(user, user2);

// Generic function for filtering objects
type Person = {
  name: string;
  age: number;
};

const users: Person[] = [
  {
    name: "abhi",
    age: 109,
  },
  {
    name: "Nahar",
    age: 109,
  },
  {
    name: "Levi",
    age: 52,
  },
  {
    name: "Random",
    age: 2,
  },
];

const filterByPeoples = <T, U extends keyof T>(
  arr: T[],
  property: U,
  value: T[U]
): T[] => {
  return arr.filter((item) => item[property] === value);
};

const filteredPeopleByName = filterByPeoples(users, "name", "Nahar");
const filteredPeopleByAge = filterByPeoples(users, "age", 109);
console.log(filteredPeopleByAge);
```
**Typescript With React**
```typescript
//Box.tsx
import { ReactNode } from "react";

type propsType = {
  heading: string;
  count?: number;
  children: ReactNode;
};

const Box = ({ heading, count = 5, children }: propsType) => {
  return (
    <>
      <h1>{heading}</h1>
      {count && <p>{count}</p>}
      {children}
    </>
  );
};

export default Box;

//App.tsx
import Box from "./components/Box";

function App() {
  return (
    <>
      <Box heading="Hello">
        {"wow, nice"}
      </Box>
    </>
  );
}

export default App;
```

**Typescript With React Hook**
```typescript
// Box.tsx
import { ThemeContext } from "../App";
import { useContext } from "react";

const Box = () => {
  const { theme, toggleTheme } = useContext(ThemeContext);
  alert(theme);
  return (
    <div
      className="box-container"
      style={{ backgroundColor: theme === "dark" ? "black" : "white" }}
    >
      <h1>Box 1</h1>
      <button onClick={toggleTheme}>Change Theme</button>
    </div>
  );
};

export default Box;


// App.tsx
import { createContext, ReactNode, useState } from "react";
import Box from "./components/Box";
type ThemeType = "light" | "dark";

interface ThemeContextType {
  theme: ThemeType;
  toggleTheme: () => void;
}

export const ThemeContext = createContext<ThemeContextType>({
  theme: "light",
  toggleTheme: () => {},
});

const ThemeProvider = ({ children }: { children: ReactNode }) => {
  const [theme, setTheme] = useState<ThemeType>("light");

  const toggleTheme = () => {
    setTheme((prev) => (prev === "light" ? "dark" : "light"));
  };

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
};
const App = () => {
  return (
    <ThemeProvider>
      <div>Hellow</div>
      <Box />
    </ThemeProvider>
  );
};

export default App;
```
**Typescript With Reducer**
```typescript
import { useReducer } from "react";

type StateType = {
  count: number;
};

type ActionType =
  | {
      type: "Increment";
      payload: number;
    }
  | {
      type: "Decrement";
      payload: number;
    };

const reducer = (state: StateType, action: ActionType): StateType => {
  switch (action.type) {
    case "Increment":
      return { count: state.count + 1 };
      break;

    case "Decrement":
      return { count: state.count - 1 };
      break;

    default:
      return state;
  }
};

const initialState: StateType = {
  count: 0,
};

const App = () => {
  const [state, dispatch] = useReducer(reducer, initialState);

  const Increment = () => {
    dispatch({
      type: "Increment",
      payload: 1,
    });
  };
  const Decrement = () => {
    dispatch({
      type: "Decrement",
      payload: 1,
    });
  };

  return (
    <div>
      <h1>Count Change</h1>
      <p>Count: {state.count}</p>

      <button onClick={Increment}>+</button>
      <button onClick={Decrement}>-</button>
    </div>
  );
};
export default App;
```



