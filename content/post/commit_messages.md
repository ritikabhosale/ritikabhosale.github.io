---
title: "How to write meaningful commits"
date: 2022-10-15T10:18:02+05:30
draft: false
---

Following git best practices is recommended and it becomes highly crucial to do so when you're working in teams on big projects. So here we'll be mainly focusing on how you can commit to make it more meaningful and helpful for others. 

**1. Use Imperative commands**  
  * Prefix your commit messages with imperative commands such as :  `fix`,`add`,`create`,`refactor`.
  * And in your commit message, tell what your changes will do, for example:
    > Add validation for username exceeding beyond 15 characters.  

    > Fix bug of user getting extra tile.

**2. Keep it Short and precise**
  * It depends on your team, what you decide is best for you, but generally, a commit message should not exceed 50 characters. 
  * Make sure your commit message clearly tells what work you did and optionally you can provide additional details if there are any such as : 
    - What effect does it have on the code base?
    - Why you did that change?
    - Is there any specific thing that the developers should watch out for while writing their code?
    - Are there are any code breaking changes?

**3. Provide Description**
  * Sometimes the commit message by itself may not tell the purpose. So consider including a commit description to give more context on what changes you made and why you did so. 
  * Here's a format of a commit message
    > Fix bug of user getting extra tile.
    > - change the sequence of steps, first player gets tile and then the turn changes
    > - fix the padding of tiles element to align it in center

**4. Make small and specific commit**
  * Remember to keep you changes specific and related. 
  * Do not make big commits with unrelated changes since it gets hard for others to understand and relate the changes. 
  * Large commits makes reverting harder. The smaller the commit, the easier and straighforward the revert.
  * If you want to revert to previous stage, you will end up losing all the changes when you make big commits.

**5. Consistency in commit messages**
  * All the developers should agree upon some common tense which you will be using when writing commit messages. 
  * Make sure you keep all the commit messages consistent which might includes tense, using proper case in sentences.
  