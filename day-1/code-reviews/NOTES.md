# Code Reviews
1. "Write the abstract of the talk you wish to attend"


## What are code reviews?
- The part in the software development process where humans review other humans' mistakes
- The code review guarantee
    - Catch mistakes in the least-costly development time.
    - Ensure the team is held accountable
    - Share domain knowledge
    - Provide opportunity to mentor, teach, and learn
    - Build a stronger foundation of trust
> The effectiveness of code review for determining faults in software is between 30% and 35% more effective than standard unit testing

You and your team get to make up the rules.

### What should you be reviewing?
- code you did not work on
- about **200-400** lines of code
- timeboxed to about an hour
> Finding bugs in code is hard.  Finding bugs in someone else's code is even harder
Create a checklist of things to review

### What should you be looking for?
- Correctness
- Clarity/maintainability
    - Can someone other than the author describe what's going on?
- Efficiency
    - Database queries
    - DOM manipulations
    - Async JS
    - using an ORM
- Style
    - Does this meet your style standards?
    - Don't waste time manually reviewing things a linter can find

### How should code reviews happen
- Have a "Code of Conduct" for how pull requests work.

## What should we be doing
**Don't**
- leave general negative feedback
    - i.e. "this is messy", "lolwut", "you'll never want to append in a loop"
- general positive feedback
    - "this looks great", "yay!", ":party-parrot:"

**Do**
- specific positive/negative feedback
- _occassionally_ give positive feedback
    - don't force it, but if you've reviewed 5 PRs and haven't said anything nice, that's probably a _code review smell_

- Assume positive intent*
    - Trust your teammates.  Be respectful.  Be humble.