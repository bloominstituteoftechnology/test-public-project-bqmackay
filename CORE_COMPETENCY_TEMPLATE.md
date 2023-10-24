## Introduction 
_The introduction should inform the learner what they'll learn and why it's important. At the very least, you should cover the following:_
- _Explain the problem or topic. Use this to provide context for the pages's title._
- _List what topics are covered in logical order._
- _Explain how and why you'll tackle the topics in 1-4 sentences._

_If you would like to use an analogy, your analogy should be ubiquitous so everyone can relate. Avoid jargon or examples that require an in-depth understanding of a scenario. Good sources for analogies may be grocery stores, riding public transit, or cooking a meal._

### Prerequisites

_List any prerequisites the learner should understand before reading your content. Select the most impactful topics and avoid listing more than three topics. Each prerequisite should be a link to a Canvas section. The link open the new page at an anchor tag._

**Example**

Before you go on, this content assumes you are comfortable with some of the past material. If needed, use the links below to return to the following topics:

- [Arrays]()

## Section Header
_The section's title describes what the learner will do at the end of the section. Use an action word as the first word. For example, "Repeating code using for loops" is a better section title than "For loops"._

_Each section contains up to four parts:_

_**Part 1: Introduction and context:** The section introduction should explain what the concept is, what it does, and why it matters. The introduction should be brief while helping the learner understand what they'll be learning._

_***Part 2: Walkthrough for implementing the concept in code:** Explain how to implement the concept in a step-by-step approach. Use simple language when covering each step. Use code examples. If the code example is long, break up the code into sections and explain each one as you go. Remember to keep the audience in mind when deciding how much detail to cover in each step._

**Example**

A for loop has three items: a starting value, a condition, and an incrementor/decrementer. Here's an example of a for loop that will loop five times:

```
for (int i = 0; i < 5; i++) { 
  /*code goes here*/ 
}
```

The starting value is int i = 0, which means the loop starts at zero. The condition is i < 5. This condition states that the loop will keep going as long as i is less than 5. Finally, the last component i++ says that after each loop, the i variable will go up by one (i.e., increment).

If we wanted to print the value of i in each loop, we could do the following:

```
for (int i = 0; i < 5; i++) { 
  // print the value of i
  System.out.println(i);
}
```

Output:
```
0
1
2
3
4
```

_**Part 3: Short video showing someone writing the code**: a brief video can help learners see how to implement a function from start to finish. The video should show a person writing the code. The person writing the code should talk through the steps they are taking. The focus of these videos is writing code. Avoid explaining other coding topics or sharing stories. Saying, "this is something I use a lot in my career," is okay, but sharing long stories should be avoided._

_**Part 4: Practice Problems Link**: Provide a link to a third-party website with practice problems. Whenever possible, use the third-party website that prescribed for the given track:_
- _Backend/Web: Replit_
- _Data Science: Google Colab_

_Practice problems should be simple, allowing learners to focus on the concept. Remember the audience when writing problems by avoiding concepts that the learner has not covered yet. Refer to the audience in the outline and the prerequisites for acceptable concepts to use in your example._

_The practice problem link should open to the page where the learner will start writing code. Learners should not have to navigate to another page after clicking on the practice problem link._

_A solution should also be available. For Replit, a solution file should be in the repl labeled "solution". For Google Colab, a separate solution link will go below the practice problem link._

## Conclusion

_At the end of each page, give the reader a summary of what they have learned. Provide encouragement and congratulations on completing the reading._
