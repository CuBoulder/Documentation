# Code Review (wip)

Borrowing liberally from [this article](https://medium.com/palantir/code-review-best-practices-19e02780015f)

## Why We Review Code

We perform code reviews (CRs) in order to improve.  Not just to improve the quality of code that we create but also to afford all of the programmers the opportunity to grow and improve through the process of reviewing and having their code reviewed.  There are several well documented benefits to formal and informal code review, for example:

- Committers are motivated to produce their best work knowing that it will be viewed by peers.  Recognition of coding expertise from peers is a source of pride for many programmers.
- Sharing knowledge helps development teams learn new techniques, solutions and algorithms as well as strengthening the institutional and project knowledge of the team.
- Consistency and legibility of merged code are necessarily improved.  
- Accidental and structural errors are more easily identified and fixed sooner.  
- Peer reviews when done properly can strengthen the bonds between team members and foster an environment where learning and growing are encouraged.

## What To Review

The general rule of thumb for our team is that you do not merge your own code.  Make a branch and commit the code and then get another member of the team to review your work and commit the change.  See : [Git workflow](HowWeWork-git_workflow)

Note that code reviews are intentionally classless - that is to say that being the most senior person on the team does not imply that your code does not need to be reviewed.  Even if, in the rare case, code is flawless, the review process affords other members of the team an opportunity for mentorship and collaboration additionally the process necessarily diversifies the understanding of the code base amongst the team.

### Get the Code for a Review

There are a some things you will need, based on the project you are reviewing, before you can begin. For example you may need a working Drupal instance, an active python virtual environment, or another project dependency. Whatever the project is, make sure that your working directory matches as closely as possible that of the author's of the PR. This way your testing will be as effective as possible.

- have your code tied to the correct remote repo for the PR
- make sure you have checked out the feature branch
- make sure you have pulled down the most recent changes
- do not make and push any changes to the code yourself
- any changes should be suggested in the PR's comments

## Preparing Code For Review

It is the author’s responsibility to submit CRs that are easy to review in order to not waste the reviewers’ time and goodwill:

- **Give Context**
  - In your PR's description or comments add links to related PRs and issues to help group related work together. There are 2 syntaxes for doing this. Github will create a short link for each to the desired issue/PR:
    - If the issue/PR to link to is in the same repository:
      - simply type: `#ISSUE_OR_PR_NUMBER`
    - If the issue/PR is in a different CuBoulder repository:
      - type: `CuBoulder/REPOSITORY_NAME#PR_NUMBER`

  - An example of something you could put in a description comment:

    ```text
    related PR: CuBoulder/Oghma#4
    ```

    Which will look like:

    - related PR: CuBoulder/Oghma#4  

- **Size and scope**
  - Changes should be narrow in scope and hand a well defined purpose.  A change may implement a new feature or fix a bug and shorter changes are preferred over longer ones.  If a CR makes substantive changes to more than a handful of files or would take more than about 20 minutes to review, consider splitting it into multiple self-contained CRs.
- **Only submit complete, self-reviews and self-tested CRs**
  - Remember that it is the responsibility of the author to make the first review.  CRs are not the place to find typos and styling issues, they should be used to validate code, find logic problems and improve collaboration and team cross-training.  
- **When refactoring code you should not alter the behavior of the code**
  - Conversely behavior-changing code should avoid refactoring code.  Each CR should attempt to follow the unix motto - do one thing and do it well.  This will help to ensure that code is reviewed correctly and efficiently.  

## Commit Messages

These messages are read to try to keep them useful. Keep it focused and informative in 72 characters or less

## Performing Code Reviews

A code review is a synchronization point among different team members and thus has the potential to block progress.  Consequently, code reviews need to be prompt (on the order of hours, not days), and team members and leads need to be aware of the time commitment and prioritize review time accordingly.  If you don’t think you can complete a review in time, please let the committer know right away so they can find someone else to do the review.  

A review should be thorough enough that you as the reviewer can explain the change at a reasonable level of detail to another developer.  This ensures that the details of the code base are known to more than a single person.  

As a reviewer, it is your responsibility to enforce WebComm coding standards and keep the quality at a high level.  Reviewing code is more of an art than a science.  The only way to learn is by doing.  Here are some things to pay attention to when performing a review of someone else’s code:

1. Purpose
    - **Does the code accomplish the stated goal?**  Every change should have a specific reason for the change (bug fix, new feature, refactor, etc.)
    - **Functions and classes should exist for a reason.** When the reason is not clear to you as the reviewer it is your responsibility to ask questions and have an understanding of why.  Consider if the code needs to be rewritten with additional comments or tests.  
2. Implementation
    - **Consider how you would have solved the problem.**  If it’s different, why is that?  Does your solution handle more (edge) cases?  Is it shorter/easier/cleaner/faster/safer and functionally equivalent?  Is there some underlying pattern that you have identified that isn’t captured by the current code?
    - **Do you see potential opportunities for abstraction?** Partially duplicated code often indicates that a more abstract or general piece of functionality can be extracted and then reused in different context.  
    - **Think like an adversary, but be nice about it.** Remember that the goal is to find problems with the code not with the coder.  Are there short-cuts that could be problematic or hard to maintain going forward?  
    - **Are established patterns and conventions being followed?** Established (and especially public) code bases should have consistent patterns and naming conventions.  It is highly desirable for new changed to follow existing patterns and conventions.  
    - **Does this change add new dependencies?** Are these additional dependencies worth the additional functionality?  Is there a way to accomplish the stated goals without adding additional third-party code?  Changes to dependencies should be scrutinized heavily.  
3. Legibility and Style
    - **Consider your reading experience.** Did you grasp the concepts in a reasonable amount of time?  Were you put off by inconsistent naming?  Were variables and code paths easy to follow?  
    - **Does the code adhere to coding guidelines and code style?** Is the code consistent with the project in terms of style, API conventions, etc.?
    - **Does this code have TODOs?** TODOs tend to just pile up in the codebase and become stale over time.  Have the author submit an issue and attach the issue number to the TODO.   The proposed code change should not contain commented-out code.
4. Maintainability
    - **Read the tests.** If there are no tests and there should be, ask the author to write some. Truly untestable features are rare, while untested implementations of features are unfortunately common. Check the tests themselves:

        - are they covering interesting cases?
        - Are they readable?
        - Does the CR lower overall test coverage? Think of ways this code could break.  
    - **Does this change break backward compatibility?** If so, is that known and accepted as a consequence of this feature being implemented? It’s fair to ask if this feature should be pushed back to a later release if there are breaking changes to existing features, API or schemas.  
    - **Leave feedback on code-level documentation, comments and commit messages.** Redundant comments clutter the code, and terse commit message mystify future contributors.  
    - **Was the external documentation updated?** If the project maintains an external documentation source, does that need to be updated to reflect this change to the code?  Check that the commit message is correctly formatted and will work with our automated CHANGELOG tools.

    Don't’ forget to praise concise/readable/efficient/elegant code.  Conversely, declining or disapproving a CR is not rude.  If the change is redundant or irrelevant, decline it with an explanation.  If you consider it unacceptable due to one or more fatal flaws, disapprove it, again with an explanation.  Sometimes the best outcome of a CR is “let’s do this a totally different way” or “do we need to do this at all.”  

    Be respectful to the code author.  While adversarial thinking is hadny, it’s not your feature and you can’t make all of the decisions.  If you can’t come to an agreement with your reviewee with code as is, switch to real-time communication or seek a third opinion.

5. Security

    Verify that the API endpoints perform appropriate authorization and authentication consistent with the rest of the code base.  Check for other common weaknesses, e.g. weak configuration, malicious user input, missing log events, etc.

6. Comments (concise, friendly, actionable)

    Reviews should be concise and written in neutral language.  Critique the code, not the author.  When something is unclear, ask for clarification rather than assuming ignorance.  Avoid possessive pronouns, in particular in conjunction with evaluations: “my code worked before your change”, “your method has a bug”, etc.  Avoid absolute judgements: “this can never work”, “the result is always wrong”.  

    Try to differentiate between suggestions (e.g. “Suggestion: extract method to improve legibility”), required changes (e.g. “Add required comment block for new class”), and points that need discussion or clarification (e.g. “Is this really the correct behavior?  If so, please add a comment explaining the logic.”).  Consider providing links or pointers to in-depth explanations of problems.  

    When you’ve finished with a code review, indicate what you expect the author to complete before you are comfortable merging the code into the code base.  Or merge the code and give the author positive feedback.  

## Responding to Reviews

Part of the purpose of the code review is to improve the author’s change request; consequently do not be offended by your reviewer’s suggestions and take them seriously, even if you don’t agree.  Respond to every comment, even if it’s only simply “acknowledged” or “done”.  Explain why you made certain decisions, why some function exists, etc.  If you can’t come to an agreement with the reviewer, switch to real-time communication or seek an outside opinion.  

Fixes should be pushed to the same branch, but in a separate commit.  Squashing commits during the review process makes it hard for the reviewer to follow up on changes.  

Tips
More tips [here](https://www.codeproject.com/Articles/524235/Codeplusreviewplusguidelines).

### Tips for the Developer

1. **The primary reviewer is the author, i.e. YOU.**
2. **Create a checklist for yourself of the things that the code reviews tend to focus on.** Some of this checklist should be easy to put together. It should follow the outline of the coding standards document. Because it’s your checklist, you can focus on the thing that you struggle with and skip the things that you rarely, if ever, have a problem with. Run through your code with the checklist and fix whatever you find. Not only will you reduce the number of things that the team finds, you’ll reduce the time to complete the code review meeting—and everyone will be happy to spend less time in the review.
3. **You are not your code.** Remember that the entire point of a review is to find problems, and problems will be found. Don’t take it personally when one is uncovered.
4. **Understand and accept that you will make mistakes.** The point is to find them early, before they make it into production. Fortunately, except for the few of us developing rocket guidance software at JPL, mistakes are rarely fatal in our industry, so we can, and should, learn, laugh, and move on.
5. **No matter how much “karate” you know, someone else will always know more.** Such an individual can teach you some new moves if you ask. Seek and accept input from others, especially when you think it’s not needed.
6. **Don’t rewrite code without consultation.** There’s a fine line between “fixing code” and “rewriting code.” Know the difference, and pursue stylistic changes within the framework of a code review, not as a lone enforcer.
7. **The only constant in the world is change.** Be open to it and accept it with a smile. Look at each change to your requirements, platform, or tool as a new challenge, not as some serious inconvenience to be fought.
8. **Fight for what you believe, but gracefully accept defeat.** Understand that sometimes your ideas will be overruled. Even if you do turn out to be right, don’t take revenge or say, “I told you so” more than a few times at most, and don’t make your dearly departed idea a martyr or rallying cry.
9. **Don’t be “the guy in the room.”** Don’t be the guy coding in the dark office emerging only to buy cola. The guy in the room is out of touch, out of sight, and out of control and has no place in an open, collaborative environment.
10. **Please note that Review meetings are NOT problem solving meetings.**
11. **Help to maintain the coding standards.** Offer to add to the coding standards for things discussed that aren’t in the coding standards. One of the challenges that a developer has in an organization with combative code review practices is that they frequently don’t know where the next problem will come from. If you document each issue into the coding standards, you can check for it with your checklist the next time you come up for code reviews. It also will help cement the concept into your mind so that you’re less likely to miss opportunities to use the feedback.

### Tips for the Reviewer

1. **Critique code instead of people – be kind to the coder, not to the code.** As much as possible, make all of your comments positive and oriented to improving the code. Relate comments to local standards, program specs, increased performance, etc.
2. **Treat people who know less than you with respect, deference, and patience.** Nontechnical people who deal with developers on a regular basis almost universally hold the opinion that we are prima donnas at best and crybabies at worst. Don’t reinforce this stereotype with anger and impatience.
3. **The only true authority stems from knowledge, not from position.** Knowledge engenders authority, and authority engenders respect – so if you want respect in an egoless environment, cultivate knowledge.
4. **Please note that Review meetings are NOT problem solving meetings.**
5. **Ask questions rather than make statements.** A statement is accusatory. “You didn’t follow the standard here” is an attack—whether intentional or not. The question, “What was the reasoning behind the approach you used?” is seeking more information. Obviously, that question can’t be said with a sarcastic or condescending tone; but, done correctly, it can often open the developer up to stating their thinking and then asking if there was a better way.
6. **Avoid the “Why” questions.** Although extremely difficult at times, avoiding the”Why” questions can substantially improve the mood. Just as a statement is accusatory—so is a why question. Most “Why” questions can be reworded to a question that doesn’t include the word “Why” and the results can be dramatic. For example, “Why didn’t you follow the standards here…” versus “What was the reasoning behind the deviation from the standards here…”
7. **Remember to praise.** The purposes of code reviews are not focused at telling developers how they can improve, and not necessarily that they did a good job. Human nature is such that we want and need to be acknowledged for our successes, not just shown our faults. Because development is necessarily a creative work that developers pour their soul into, it often can be close to their hearts. This makes the need for praise even more critical.
8. **Make sure you have good coding standards to reference.** Code reviews find their foundation in the coding standards of the organization. Coding standards are supposed to be the shared agreement that the developers have with one another to produce quality, maintainable code. If you’re discussing an item that isn’t in your coding standards, you have some work to do to get the item in the coding standards. You should regularly ask yourself whether the item being discussed is in your coding standards.
9. **Remember that there is often more than one way to approach a solution.** Although the developer might have coded something differently from how you would have, it isn’t necessarily wrong. The goal is quality, maintainable code. If it meets those goals and follows the coding standards, that’s all you can ask for.
10. **You shouldn’t rush through a code review - but also, you need to do it promptly.** Your coworkers are waiting for you.
11. **Review fewer than 200-400 lines of code at a time.**

## Collaborative Formal Code Reviews

Periodically (monthly, quarterly, semesterly???) the Development and DevOps teams (anyone else from the Constituent Experience and Technology team is welcome to attend) will join a larger in-person Code Review.  While nominally called a Code Review the purpose of this more formal meeting isn’t to catch bugs and enforce norms, rather it is an opportunity for the developers to share interesting solutions, novel problems as well as introduce new technologies to the larger team.  Cross-training and continuous education is the desired outcome.

Developers are encouraged to tag interesting solutions or novel algorithms in their code with the review tag (tbd).  Ideally everyone who commits code would have a few minutes to share something with the larger group.  While not explicitly intended as a problem-solving or brainstorming exercise, asking for general tips or strategies is permissible.  

Occasionally there may be additional ad-hoc Code Review meetings designed to explore new technologies that may directly impact the WebComm team in the near future.  Ideally someone on the team or multiple members of the team would take on the task of doing a pro/con analysis for several competing or emerging technologies to determine which one makes the most sense for adoption for production use.  
