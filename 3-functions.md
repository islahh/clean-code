## Small!
The first rule of functions is that they should be small. The second rule of functions is that
they should be smaller than that. Functions should hardly ever be 20 lines long.

Ideally, Every function to be just two, or three, or four lines long. Each to be transparently obvious. Each tell
a story. And each led you to the next in a compelling order. That’s how short your functions
should be

## Blocks and Indenting
This implies that the blocks within if statements, else statements, while statements, and
so on should be one line long. Probably that line should be a function call with a nicely descriptive name.

This also implies that functions should not be large enough to hold nested structures.
Therefore, the indent level of a function should not be greater than one or two. This, of
course, makes the functions easier to read and understand.

## Do One Thing
**FUNCTIONS SHOULD DO ONE THING. THEY SHOULD DO IT WELL.
THEY SHOULD DO IT ONLY.**

One way to know that a function is doing more than “one thing” is if you can
extract another function from it with a name that is not merely a restatement of its implementation.

Additionally, Functions that do one thing cannot be reasonably divided into
sections such as declarations, initializations, and sieve. This is an obvious symptom of
doing more than one thing.

Don’t be afraid to spend time choosing a name. Indeed, you should try several different
names and read the code with each in place.
Be consistent in your names. Use the same phrases, nouns, and verbs in the function
names you choose for your modules. Consider, for example, the names includeSetup-
AndTeardownPages, includeSetupPages, includeSuiteSetupPage, and includeSetupPage.

In order to make sure our functions are doing “one thing,” we need to make sure that the
statements within our function are all at the same level of abstraction.
`TODO: PROVIDE A JS EXAMPLE.`

# Reiterate
### Reading Code from Top to Bottom: The Stepdown Rule
We want the code to read like a top-down narrative.5 We want every function to be followed
by those at the next level of abstraction so that we can read the program, descending
one level of abstraction at a time as we read down the list of functions. I call this The Stepdown
Rule.
To say this differently, we want to be able to read the program as though it were a set
of TO paragraphs, each of which is describing the current level of abstraction and referencing
subsequent TO paragraphs at the next level down.
To include the setups and teardowns, we include setups, then we include the test page content,
and then we include the teardowns.
To include the setups, we include the suite setup if this is a suite, then we include the
regular setup.
To include the suite setup, we search the parent hierarchy for the “SuiteSetUp” page
and add an include statement with the path of that page.
To search the parent. . .
It turns out to be very difficult for programmers to learn to follow this rule and write
functions that stay at a single level of abstraction. But learning this trick is also very
important. It is the key to keeping functions short and making sure they do “one thing.”
Making the code read like a top-down set of TO paragraphs is an effective technique for
keeping the abstraction level consistent.
Take a look at Listing 3-7 at the end of this chapter. It shows the whole
testableHtml function refactored according to the principles described here. Notice
how each function introduces the next, and each function remains at a consistent level
of abstraction.


## Function Arguments
The ideal number of arguments for a function is zero (niladic). Next comes one (monadic), followed
closely by two (dyadic). Three arguments (triadic) should be avoided where possible. More than three
(polyadic) requires very special justification—and then shouldn’t be used anyway.

Imagine the difficulty of writing all the test cases to ensure that all the various combinations of arguments work
properly. If there are no arguments, this is trivial. If there’s one argument, it’s not too hard.
With two arguments the problem gets a bit more challenging. With more than two arguments,
testing every combination of appropriate values can be daunting.

# Have No Side Effects
Side effects are lies. Your function promises to do one thing, but it also does other hidden
things.

`TODO`: turn it into JS example
``` bash
UserValidator.java
public class UserValidator {
private Cryptographer cryptographer;
public boolean checkPassword(String userName, String password) {
User user = UserGateway.findByName(userName);
if (user != User.NULL) {
String codedPhrase = user.getPhraseEncodedByPassword();
String phrase = cryptographer.decrypt(codedPhrase, password);
if ("Valid Password".equals(phrase)) {
Session.initialize();
return true;
}
}
return false;
}
}
```
The side effect is the call to Session.initialize(), of course. The checkPassword function,
by its name, says that it checks the password. The name does not imply that it initializes
the session.

# Prefer Exceptions to Returning Error Codes
Returning error codes from command functions is a subtle violation of command query
separation. It promotes commands being used as expressions in the predicates of if statements.
if (deletePage(page) == E_OK)
This does not suffer from verb/adjective confusion but does lead to deeply nested structures.
When you return an error code, you create the problem that the caller must deal with
the error immediately.
if (deletePage(page) == E_OK) {
if (registry.deleteReference(page.name) == E_OK) {
if (configKeys.deleteKey(page.name.makeKey()) == E_OK){
logger.log("page deleted");
} else {
logger.log("configKey not deleted");
}
} else {
logger.log("deleteReference from registry failed");
}
} else {
logger.log("delete failed");
return E_ERROR;
}
On the other hand, if you use exceptions instead of returned error codes, then the error
processing code can be separated from the happy path code and can be simplified:
try {
deletePage(page);
registry.deleteReference(page.name);
configKeys.deleteKey(page.name.makeKey());
}
catch (Exception e) {
logger.log(e.getMessage());
}

## Extract Try/Catch Blocks
Try/catch blocks are ugly in their own right. They confuse the structure of the code and
mix error processing with normal processing. So it is better to extract the bodies of the try
and catch blocks out into functions of their own.

``` bash
public void delete(Page page) {
try {
deletePageAndAllReferences(page);
}
catch (Exception e) {
logError(e);
}
}
private void deletePageAndAllReferences(Page page) throws Exception {
deletePage(page);
registry.deleteReference(page.name);
configKeys.deleteKey(page.name.makeKey());
}
private void logError(Exception e) {
logger.log(e.getMessage());
}
```
In the above, the delete function is all about error processing. It is easy to understand
and then ignore. The deletePageAndAllReferences function is all about the processes of
fully deleting a page. Error handling can be ignored. This provides a nice separation that
makes the code easier to understand and modify.

## Error Handling Is One Thing
Functions should do one thing. Error handing is one thing. Thus, a function that handles
errors should do nothing else. This implies (as in the example above) that if the keyword
try exists in a function, it should be the very first word in the function and that there
should be nothing after the catch/finally blocks.

## How Do You Write Functions Like This?
Writing software is like any other kind of writing. When you write a paper or an article,
you get your thoughts down first, then you massage it until it reads well. The first draft
might be clumsy and disorganized, so you wordsmith it and restructure it and refine it until
it reads the way you want it to read.
When I write functions, they come out long and complicated. They have lots of
indenting and nested loops. They have long argument lists. The names are arbitrary, and
there is duplicated code. But I also have a suite of unit tests that cover every one of those
clumsy lines of code.
So then I massage and refine that code, splitting out functions, changing names, eliminating
duplication. I shrink the methods and reorder them. Sometimes I break out whole
classes, all the while keeping the tests passing.
In the end, I wind up with functions that follow the rules I’ve laid down in this chapter.
I don’t write them that way to start. I don’t think anyone could.
