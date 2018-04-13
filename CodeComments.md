## // Code Comments
Comments are, at best, a necessary evil. The proper use of comments is to compensate for our failure to express ourselves in code. Note that I used the word failure. I meant it. Comments are always failures. We must have them because we cannot always figure out how to express ourselves without them, but their use is not a cause for celebration. <br/> 

When you find yourself in a position where you need to write a comment, think it through and see whether there is some way to express yourself in code instead. Every time you express yourself in code, you should pat yourself on the back. Every time you write a comment, you should grimace and feel the failure of your ability of expression. <br/>

<h3> Comments lie </h3> 
Comments lie. Not always, and not intentionally, but too often nevertheless. Code changes and evolves. Unfortunately the comments don’t always keep up and become orphaned blurbs of ever decreasing accuracy. <br/>

You might be thinking “programmers should be disciplined enough to keep the comments up to date”. I agree, they should. But they won’t. <br/>

Inaccurate comments are worse than no comments at all. They mislead, set expectations that will never be fulfilled, lay down obsolete rules and specification. Truth can only be found in one place: the code. It is the only source of truly accurate information. <br/>

<h3> Comments Do Not Make Up for Bad Code </h3>

One of the more common motivations for writing comments is bad code. We write a module and we know it is confusing and disorganized. We know it’s a mess. <br/>

So we say to ourselves, “Ooh, I’d better comment that!” <br/>
No! You’d better clean it! <br/>

<h3> Explain Yourself in Code </h3>

Which would you rather see? <br/> 

```// Check to see if the employee is eligible for full benefits 
if ((employee.flags & HOURLY_FLAG) && (employee.age > 65))
{
   ...
}
```
OR

```
if (employee.IsEligibleForFullBenefits())
{
   ....
}
```

Often you need less than a minute to think and explain your intent in code. In many cases, all you need to do, is creating a function with a name that says the same thing as the comment you want to write! <br/>

<h4> Informative Comments </h4> 

It is sometimes useful to provide basic information with a comment. For example: <br/> 

```
// format matched kk:mm:ss EEE, MMM dd, yyyy
var timeMatcher = new Regex("\\d*:\\d*:\\d* \\w*, \\w* \\d*, \\d*");
```

In this case the comment lets us know that the regular expression is intended to match a time and date. <br/>

Even in this example, it would have been better to define a string constant named DateTimeRegexFormat, instead of a comment. <br/>

<h4> Explanation of Intent </h4>
Sometimes a comment goes beyond just the implementation and provides the intent behind a decision. For example: <br/>

```
public void TestConcurrentAddWidgets()
{
    ...

    // This is our best attempt to get a race condition by creating large number of threads:

    for (int i = 0; i < 25000; i++) 
    {
         var action = new WidgetBuilderThread(...);
        Thread.Start(action);
    }

    assertEquals(...);
}
```

<h4> Clarification </h4>

When using libraries and code that you cannot change and clean up, you can use comments to clarify the meaning of obscure arguments or return value. For example: <br/> 

```
assertTrue(a.compareTo(b) != 0);    // a != b
assertTrue(a.compareTo(b) == 0);  // a == b
assertTrue(a.compareTo(b) == -1);   // a < b
```


<h4> Warning of Consequences </h4>
Sometimes it is useful to warn other programmers about certain consequences. For example, a comment can specify whether a class or method is thread safe. <br/>

<h4> TODO Comments </h4> 
It is sometimes reasonable to leave reminders and action notes in the form of // TODO comments. TODOs are jobs that you think should be done, but for some reason can’t do at the moment. For example: <br/>

```
// TODO: We expect this to be removed when ...
protected VersionInfo MakeVersion()
{ 
      return null;
}
```

Visual Studio can locate all the TODO comments and show them as messages in the error window, so it’s not likely that they will get lost. <br/>


<h4> XML Docs vs Comments </h4>

When the comments relate to a class, method or a method argument, then write the comments as XML documentation. This allows callers to immediately notice them using intellisense without having to look at your code. <br/> 

```
/// <summary> comments here </summary>
public void Something()
{
     ...
}
```

<h3> Bad Comments </h3> 

Most comments fall into this category. Usually they are crutches or excuses for poor code or justifications for insufficient decisions, amounting to little more than the programmer talking to himself. <br/>

<h4> Avoid Mumbling </h4>
Comments are meant to be understandable by other people. When you write a comment, read it again. Make sure that it makes sense for other people that are not in your head. <br/>

<h4> Redundant Comments </h4>
Avoid comments that essentially just repeat what the code does in plain English. They probably take longer to read than the code itself. <br/>


Remember that anyone reading that comment will be a programmer and so will naturally read the code too anyway. <br/>

Such comments will be less precise than the code and, when they get out of sync in the future, will just cause confusion, or worse, mislead the poor reader. <br/>

<h4> Mandated Comments </h4> 
Some companies have a rule that says that every function must have xml documentation, or every variable must have a comment. That’s plain silly for the reasons explained above. <br/>

Unfortunately, there is an evil warning code 1591 in Visual Studio which kicks in when you enable XML documentation file generation in the build settings of a project. It prompts you to add xml comments to everything that is public. Do not obey that. Instead, suppress the rule code in the project build settings. <br/> 



<h4> Replace comments with methods or variables </h4>

Consider the following code: <br/> 

```
// Can the order be submitted?
If (basket.Total > 0 && basket.Items.All(x => x.IsAvailable())
{
   ....
}

``` 
It could be written without comments as: <br/> 

```
var canBeSubmitted = 
   basket.Total > 0 && basket.Items.All(x=>x.IsAvailable());
if (canBeSubmitted)
{
   ....
}
```

The same technique can be used with methods. Methods are preferred to variables when the implementation logic is a bit more complicated or when the concept is reusable. In the above example, a method named canBeSubmitted() defines on the Basket class would have been more clear. <br/>

<h4> Function Headers </h4>

Short functions don’t need much description. A well-chosen name for a small function that does one thing is usually better than a comment header. <br/>

<h4> Commented-Out Code </h4>

Sometimes you want to temporarily comment out some code and try an alternative implementation. Or you think something is unnecessary and you want to delete it, but half heartedly. <br/>

Others who see that commented-out code won’t have the courage to delete it. They’ll think it is there for a reason and is too important to delete. So commented-out code accumulates like dirt. <br/>

You should never push commented out code into GIT. If you are happy enough with the changes that you want to check them into the repository, just delete the commented out code before you do. <br/>