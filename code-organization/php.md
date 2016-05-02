# PHP Code Organization

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Organization](#organization)
  - [Group by Component (aka Context, Module, Or Feature)](#group-by-component-aka-context-module-or-feature)
    - [Sub-contexts](#sub-contexts)
  - [Group by Type (aka Pattern)](#group-by-type-aka-pattern)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->


## Organization

[Matt Stauffer's article](https://mattstauffer.co/blog/how-to-organize-class-namespaces) on organization outlines the different approaches quite well.

The preferred organization structure is [Component](#group-by-component-aka-context-or-module) since it scales well, is similar to our javascript organization structure, allows for easier code reviews, and is easier to conceptually associate the different parts of a code base.


Grouping by [Type](#group-by-type-aka-pattern) starts to break down in larger code bases and does not offer any significant benefits over grouping by component.  A combination of the two approaches is possible but would need to be evaluated on a case-by-case basis.

### Group by Component (aka Context, Module, Or Feature)

Notice how it is easy to find all the code related to a feature:

```
src
    Billing
        Receipt (model)
        ReceiptRepository
        SendReceipt (command)
        SendReceiptHandler (event handler)
        BillingServiceProvider
    User
        User (model)
        UserRepository
        CreateUser (command)
        CreateUserHandler (event handler)
        UserServiceProvider
```

#### Sub-contexts

A further refinement of this approach in larger code bases is to add sub-context folders:


```
src
    Billing
        Receipt
            Receipt
            ReceiptRepository
            SendReceipt
            SendReceiptHandler
        Order
            ...other files here...
    User
        User
        UserRepository
        CreateUser
        CreateUserHandler
```




These don't necessarily match up with frontend endpoints.

### Group by Type (aka Pattern)

This pattern works for smaller code bases but conceptually it has disadvantages in that
it requires you to hunt for all of the files related to a component.  

```
src
    Commands
        SendReceipt
        CreateUser
    Entities
        Receipt
        User
    Handlers
        SendReceiptHandler
        CreateUserHandler
    Repositories
        ReceiptRepository
        UserRepository
```
