# Welcome to Grokking Simplicity

## Aims
- Learn the definition of functional thinking
- Discover the primary distinction that functional programmers make when they look at code

## What is functional programming (FP)?

### Definitions

#### Dictionary definitions
1. A programming paradigm characterised by the use of mathematical functions and the avoidance of side effects.
2. A programming style that uses only pure functions without side effects.



### Side effects
> Anything a function does other than returning a value.

For example: sending an email, or modifying global state.

### Pure functions
> Functions that depend only on their arguments and don't have any side effects.

Equivalent to _mathematical functions_.

## Distinguishing actions, calculations, and data

Below are code snippets from an existing codebase. You need to be more careful with the snippets with warnings (⚠️):

```swift
{
  "firstName": "Eric",
  "lastName": "Normand"
}

⚠️ sendEmail(to:from:subject:body)

sum(numbers)

⚠️ saveUserToDatabase(user)

stringLength(string)

⚠️ getCurrentTime()

[1, 10, 2, 45, 3, 98]
```

The functions with warnings (⚠️) need caution because they depend on when they're run and how many times they're run.

For example, you don't want to send an important email twice or zero times.

These annotated snippets are _actions_.

### Distinguishing code that matters when you call it

A simplified definition of an action is "code that matters when you call it".

Let's separate the code in the code snippet:

```swift
// Actions
sendEmail(to:from:subject:body)
saveUserToDatabase(user)
getCurrentTime()

// Other code
{ "firstName": "Eric",
  "lastName": "Normand" }

sum(numbers)

stringLength(string)

[1, 10, 2, 45, 3, 98]
```

### Distinguishing inert data from code that does work

Neither "calculations" nor "data" depend on when or how many times they're used.

The difference: calculations can be executed, data cannot.

Let's further separate the code in the code snippet for calculations and data:

```swift
// Actions
sendEmail(to:from:subject:body)
saveUserToDatabase(user)
getCurrentTime()

// Calculations
sum(numbers)
stringLength(string)

// Data
{ "firstName": "Eric",
  "lastName": "Normand" }

[1, 10, 2, 45, 3, 98]
```

In general, a functional programmer prefers data to calculations and prefers calculations to actions.

### Example: cloud service for project management

When a client marks their tasks as completed, a central server sends email notifications.

#### Step 1: User marks task as completed
This triggers a UI event. A UI event is an _action_ because it depends on how many times it happens.

#### Step 2: Client sends message to server
Sending a message is an _action_ because it depends on how many times it happens.
The message itself is _data_, because it is inert bytes that must be interpreted.

#### Step 3: Server receives message
Receiving a message is an _action_ because it depends on how many times it happens.

#### Step 4: Server makes change to its database
Changing the internal state is an _action_.

#### Step 5: Server decides who to notify
Making a decision is a _calculation_. Given the same inputs, the server would make the same decision.

#### Step 6: Server sends email notification
Sending an email is an _action_ because it depends on how many times it happens.
(Why? Because sending the same email twice is different to sending it once)

### Tools for working with actions, calculations, and data

#### Actions
Tools for:
* Safely changing state over time
* Guaranteeing ordering
* Ensuring actions happen exactly once

#### Calculations
Tools for:
* Static analysis to aid correctness
* Mathematical tools that work well for software (what does this mean?)
* Testing strategies

#### Data
Tools for:
* Organising data for efficient access
* Keeping records long term
* Capturing what is important using data

## How does distinguishing actions, calculations, and data help us?

Functional programming works great for distributed systems, and most software written today is distributed.

In the mobile space: our apps (client) must communicate with backend servers in a distributed way.

### Three rules of distributed systems
1. Messages can arrive out of order
2. Each message may arrive 0, 1, or 2+ times (never, once, many)
3. If you don't hear back, you don't know what happened

## What is functional thinking?

The set of skills and ideas that functional programmers use to solve problems with software.

Two of those skills and ideas are:

### 1. Distinguishing between actions, calculations, and data
These three categories correspond to how difficult code is to understand, test, and reuse.

### 2. Using first-class abstractions
Finding common procedures and naming them to be reused later, especially by passing in procedures (closures) to the procedures (functions).
