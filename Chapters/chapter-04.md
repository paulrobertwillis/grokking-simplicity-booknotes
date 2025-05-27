# Extracting calculations from actions

Actions, Calculations, Data

Action
Anything that has an effect on the world or is affected by the world. As a rule of thumb, actions depend on when or how many times they are run.

Actions are also sometimes called “impure functions”, “side-effecting functions”, or “functions with side effects”.

Calculation
Computation from inputs to outputs. Doesn’t affect anything outside itself, so doesn’t depend on when or how many times it’s run.

Data
Facts about events. Recorded immutably since facts don’t change.

Some ways to deal with actions
1. Use fewer actions if possible.
2. Keep actions small.
3. Restrict actions to interactions with the outside.
4. Limit dependence on time (when, or how many times action runs).

Improving testability and reusability
* Separate business rules from “DOM” (Domain Object Model) updates.
* Remove and avoid global variables.
* Don’t assume the answer goes in the DOM. (In iOS dev, would this be assuming a function should set a value on an object?)
* Return the result from the function.

Transforming an action into a calculation
Every function has inputs and outputs. These can be implicit or explicit.

Explicit inputs are arguments.
Explicit outputs are return values.

Any other way information enters or leaves the function is implicit.

1. Isolate calculation code

We can see that there’s a block of code in the below `calculateCartTotal()` function that does the work of calculation the total. We can extract it to its own function before modifying it.

Original
```swift
var shoppingCart: [Item] = []
var shoppingCartTotal = 0.0

func calculateCartTotal() {
    shoppingCartTotal = 0.0
    for item in shoppingCart {
        shoppingCartTotal += item.price
    }

    setCartTotal()
    updateShippingIcons()
    updateTax()
}
```

Extracted
```swift
var shoppingCart: [Item] = []
var shoppingCartTotal = 0.0

func calculateCartTotal() {
    calculateTotal()
    setCartTotal()
    updateShippingIcons()
    updateTax()
}

func calculateTotal() {
    shoppingCartTotal = 0.0
    for item in shoppingCart {
        shoppingCartTotal += item.price
    }
}
```

2. Convert its implicit inputs to arguments and implicit outputs to return values

