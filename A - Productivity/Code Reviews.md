  

Tips for effective software engineering code reviews:

As an author, value your reviewer's time. For respectful code reviews:  

• Review your code yourself first  

• Break up large change-lists / pull requests  

• Automate the easy stuff (linting, formatting)  

• Narrowly scope changes  

• Respond graciously to critique  

• Minimize lag between rounds of review  

• Artfully solicit missing information  

• Communicate responses explicitly  

• Don’t forget the docs. Good documentation contains context that is missing from the code. It’s doesn’t just repeat it.  

• Discuss things upfront where it makes sense to. Design docs and team meetings can be great for aligning on API semantics, implementation details etc. prior to the code review and can avoid exceptionally long review cycles.  

As a reviewer, check that code is…  

• Required. Is the code needed?  

• Well designed (e.g. how well do the various pieces interact together? how well do they interact with the system as a whole?)  

• Readable by others  

• Doing what the author intended (and is the intention good for both end-users and maintainers?)  

• No more complex than needed (e.g. can it be understood quickly? are folks very likely to add bugs when modifying it?)  

• Commented with the why vs. what (explain why code exists vs what its doing if possible)  

• Following the style guide (ideally automate enforcement, code with major style changes (e.g. reformats) should be kept separate)  

• Has appropriate tests that are designed well  

• Sufficiently documented in the same PR (keeps the docs fresh, and helps explain what you're doing)  

...and keep code reviews constructive!  

• Comments should be about the code, not the developer.  

• Programming skill evaluations don’t belong in code reviews.  

• Don’t ask condescending questions. Common examples of the genre include “Why did you do this?”  

• Write clear and specific comments.  

• Include positive feedback.  

• Avoid overly nitpicking. Lean on automatic style checking for this.  

• Let computers do the boring parts  

• Settle style arguments with a style guide  

• Start reviewing immediately  

• Start high level and work your way down  

• Be generous with code examples  

• Frame feedback as requests, not commands  

• Tie notes to principles, not opinions  

Related reading:  

• How to Make Your Code Reviewer Fall in Love with You - [https://lnkd.in/g66DW_mm](https://lnkd.in/g66DW_mm)  

• Code Review Best Practices That Will Boost Team Morale - [https://lnkd.in/gh_t8kmK](https://lnkd.in/gh_t8kmK)  

• The Code Review Pyramid - [https://lnkd.in/gjEFuunw](https://lnkd.in/gjEFuunw)