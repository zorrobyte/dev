Scientific Paper Notes
===

0. Abstract
1. Introduction
2. Background
3. Design and Algorithm
4. Results
5. Conclusions

---

### Ernst notes

Micael Ernst ["How to write a technical paper or a research paper"](https://homes.cs.washington.edu/~mernst/advice/write-technical-paper.html).

* Purpose of science is to communicate ideas and to share knowledge, not just to discover it
* know your message, stay on message
  - important - show why the problem is important
  - hard - obvious techniques fail, existing approaches do not work, show what others have tried and failed
  - solved - problem has been solved, give evidence and show work of how and why it was solved
  - knowing reader determines points of interest
  - what it is and why it works
* details
  - communciate specific ideas
  - cut out irrelevant detail
  - communicate what would be most interesting to reader, not yourself
  - do not weight prose by time and effort spent, communicate the relevant successes
  - if failures are communicated, frame it as a warning to not go down blind alleys
  - if several approaches, communicate best one first and give alternatives after
    + consider not giving alternatives at all if not relevant
* organization
  - communicate main ideas early and clearly (give away the punchline)
  - anti-pattern: mass of detail at the beginning with conclusion at end
  - state point first, then support it
  - consider giving mini-introductions about organization
    + whole paper 1 paragraph
    + section 1 setence
  - writing abstract and intro first helps with paper writing and organization
  - writing rest of paper first helps writing abstrant and intro later
  - writing abstract and intro first will most likely be less effort to write paper
    as abstrant and intro are shorter and provide roadmap for paper
  - provide what task is, or what goal is, as motivation for technical details
* getting started
  - talk it out
  - outline
  - stream of conscious notes
  - write in parts, whichever is desired
  - copy from yourself, use what you have already written in other parts to get started
* brevity
  - write succinctly
  - cut out extraneous detail, sections, words, etc.
  - each section should contribute to papers point
  - each paragraph should have one point
  - each sentence should support the paragraphs one point
  - delete if any of those three points is not satisfied
* style
  - do not use passive voice ("the tree was pulled" - passive, "someone pulled the tree" - active)
  - first person should be rarely used
  - do not use 'we' to mean reader and author
  - do not use 'we' to describe execution of program or idea ("we compute a graph" - no)
  - do not anthropomorphise programs
  - avoid adjectives
  - don't overuse 'novel'
  - do not use 'clearly', 'easily', 'obviously', 'trivial'
  - prefer singular ("sequences induce graphs" -> "each sequence induces a graph")
  - describing experiments should be past tense
  - describing paper itself, use present tense
  - avoid gratuitous use of future tense ("switching wires will cause an error" -> "switching wires causes an error")
  - use redundant commas ("milk, cheese and crackers" -> "milk, cheese, and crackers")
  - english has compound adjectives but not nouns
  - avoid ambious words. (as, since -> because) (whether -> if)
  - avoid quotation, paraphrasings usually suffice
* figures
  - example figures help clarify ideas
  - figures should stand on their own
  - use consistent pictoral elements, with only two different types of arrows (boxes, shading, etc.)
  - use a legend if more than two types of style elements
  - all graphs, diagrams, screenshots, etc. should be named figures
  - put figures at top of page
  - don't waste text that is more concise in the figure (don't repeat numbers in figure in text, etc.)
* naming
  - give concepts names (as opposed to "approach 1", "approach 2", etc.)
  - better to name on what it does than how
  - avoid elegant variations
    + don't substitute "program", "library", "component", "system", "artifact" with each other, stick to one and use it consistently
    + don't substitute "program", "code", "source" with each other, stick to one and use it consistently
  - do not use single term to refer to multiple concepts ("phase" when describing algorithm, "step" when describing a tool use)
  - use consistent list semantics ("three reasons... one, ..., two, ..., three ...")
  - try to use precise terms (bug -> fault, defect, bug report, etc.) (https://en.wikipedia.org/wiki/Dependability)
* numbers and measurement
  - ...
* compilation
  - document compilation steps, preferably making it automated 
* related work
  - section should explain what others have done but should be compared and contrasted with your work
  - provide context presented related work
  - better to defer limitations of your technique to later sections
* feedback
  - get feedback
* submission
  - err on submitting too late than too early
  - rule of thumb is to submit if you're proud of paper in current form
  - don't submit if it's known that reviewers will have significant criticisms
  

### Dreyer writing notes

Derek Dreyer ["How to Write Papers So People Can Read Them"](https://www.youtube.com/watch?v=L_6xoMjFr70)

* flow
  -  old to new
    + begin sentences with old information and end with new
* coherence
  - one paragraph one point
    + main point should be expressed in a single point sentence
    + typically near beginning of paragraph
* give unique names to things and use them consistently
* give information precisely, when its needed, not before
* research paper structure
  - abstract, 1-2 paragraphs 1k readers
  - intro, 1-2 pages, 100 readers
  - main ideas, 2-3 pages, 50 readers
  - technical meat, 4-6 pages, 5 readers
  - related work, 1-2 pages, 100 readers
* cgi
  - context: motivate topic
  - gap: explain specific problem and why existing work does not solve it
  - innovation: what's new and fill gap
* intro
  - expanded version of abstract
* main idea
  - concreate illustrative examples
  - do not show general solution
* related work
  - goes at end
  - give real comparisons, explain how your research fills in the gap

### 7 research paper suggestions

Simon Peyton Jones ["How to write a great research paper"](https://www.youtube.com/watch?v=VK51E3gHENc)

1. don't wait: write
2. identify your key idea
3. tell a story
4. nail your contributions
5. related work: later
6. put your readers first (examples)
7. listen to your readers

---

* write, even if you haven't done or started the work of research
  - (idea,paper,research) not (idea,research,paper)
* identify your key idea
  - convey useful and re-usable idea
  - you don't need a fantastic idea before you can write a paper
  - your paper should have on clear, sharp idea
  - lots of ideas should be lots of papers
  - do not leave the reader in doubt of what your idea is, be explicit
* conference paper structure
  - title, 1k readers
  - abstract, 4 sentences, 100 readers
  - intro, 1 page, 100 readers
  - problem, 1 page, 10 readers
  - new ideas, 2 pages, 10 readers
  - details, 5 pages, 3 readers
  - related work, 1-2 pages, 10 readers
  - conclusion/future work, 0.5 pages
* introduction
  - describe problem
  - state contributions
  - that's it
  - one page
* molehills not mountains
* contributions
  - write list of contributsion first
  - contributions drive paper
  - allows reader to determine if rest of paper is worth reading
  - don't leave the reader to guess what contributions are
  - good methodology is to put bullet points of concreate contributions
* don't give what you will do in forward sections, give forward references
  to sections after making claims ("in section 2 we will show ...", "show show that ... (section 2)")
* related work should go at the end
* leading the reader to your idea can pass through related work and should be expanded on and given
  credit, but the main focus is on idea exposition, not on reviewing what has been done in the field
* give credit where its due
* be generous to the competition
* acknowledge weakness in your approach
  - on the path to the idea (intro), you can mention what your focus is while acknowledging
    what the focus is not (what its not good at) and forward reference to related work
    ("axe is good for cutting trees but not vegetables, we focus on cutting trees and mention
    vegetables in related works")
* present ideas and convey intuition
  - give examples then present general case

### Pattersons writing advice

["Dave Patterson's Writing Advice"](https://people.eecs.berkeley.edu/~pattrsn/talks/writingtips.html).

* active voice ("as shown in fig x" -> "fig x shows")
* eliminate "this" ambiguities ("this" -> "this is ...", "this <noun> ...")
* "while" should only refer to time ("while" -> "although")
* single numbered sections are superfluous
* capitalize chapter, figure and table references ("Figure 1", "Chapter 3")
* % for percentages, $ for dollars
* spell out one to ten, numerals for 11 and up
  - exception when arithmetic is involved ("8 core, 4 computer -> 32 processors")
* INSPEC

References
---

* SIGPLAN [Author Information](https://www.sigplan.org/Resources/Author/)
