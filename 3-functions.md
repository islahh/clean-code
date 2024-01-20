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
