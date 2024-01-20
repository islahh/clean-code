## Use Intention-Revealing Names
Choosing good names takes time but saves more than it takes.The name of a variable, function, or class, should answer all the big questions. It
should tell you why it exists, what it does, and how it is used. If a name requires a comment,
then the name does not reveal its intent.
```bash
int d; // elapsed time in days
```

The name d reveals nothing, instead we can use a name that reveal intend
```bash
int elapsedTimeInDays;
int daysSinceCreation;
int daysSinceModification;
int fileAgeInDays;
```

## Avoid Disinformation
Do not refer to a grouping of accounts as an accountList unless it’s actually a List.
The word list means something specific to programmers. If the container holding the
accounts is not actually a List, it may lead to false conclusions. So accountGroup or
bunchOfAccounts or just plain accounts would be better.

## Make Meaningful Distinctions
It is not sufficient to add number series or noise words, even though the compiler is
satisfied. If names must be different, then they should also mean something different.
int account
int accounts
int accnts
Means the same thing, these should not be considered as three different variables.

## Use Pronounceable Names
Number-series naming (a1, a2, .. aN) is the opposite of intentional naming. Such
names are not disinformative—they are noninformative; they provide no clue to the
author’s intention.

If you can’t pronounce it, you can’t discuss it without sounding like an idiot. “Well,
over here on the bee cee arr three cee enn tee we have a pee ess zee kyew int, see?” This
matters because programming is a social activity

## Use Searchable Names
Single-letter names and numeric constants have a particular problem in that they are not
easy to locate across a body of text. On the other hand, One might easily grep for MAX_CLASSES_PER_STUDENT,

My personal preference is that single-letter names can ONLY be used as local variables
inside short methods. The length of a name should correspond to the size of its scope

`One difference between a smart programmer and a professional programmer is that
the professional understands that clarity is king. Professionals use their powers for good
and write code that others can understand.`

## Class Names
Classes and objects should have noun or noun phrase names like Customer, WikiPage,
Account, and AddressParser. Avoid words like Manager, Processor, Data, or Info in the name
of a class. A class name should not be a verb.

## Method Names
Methods should have verb or verb phrase names like postPayment, deletePage, or save.
Accessors, mutators, and predicates should be named for their value and prefixed with get,
set.
```bash
string name = employee.getName();
customer.setName("mike");
if (paycheck.isPosted())...
```
## Don’t Pun
Avoid using the same word for two purposes. Using the same term for two different ideas
is essentially a pun.

For instance: Let’s say we have many classes where add will create a
new value by adding or concatenating two existing values. Now let’s say we are writing a
new class that has a method that puts its single parameter into a collection. Should we call
this method add? It might seem consistent because we have so many other add methods,
but in this case, the semantics are different, so we should use a name like insert or append
instead. To call the new method add would be a pun.
