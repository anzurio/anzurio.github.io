## The Importance of Requirement Gathering, Framework Design and Unit Testing [^1]

[^1]: Originally written for Propelics and currently [posted](https://www.anexinet.com/blog/the-importance-of-requirements-gathering-framework-design-and-unit-testing/) at Anexinet's Blog.

In an age of ever-changing requirements, rapidly evolving technology, and discussions over tabs or spaces, never forget the importance of requirements gathering, framework design, and unit testing. These often involve many players: from the clichéd client who doesn’t know what he wants, the product manager who only budgeted for code production, the lead software development engineer who didn’t account for requirement changes, to the developer who feels unit testing is a waste of time and is eager to start writing code.

These challenges may have been exacerbated by a misinterpretation of the Agile Software Development Methodology. Specifically, its principles and values have been cherry-picked, and in some cases, butchered. Here’s a few examples:

- Value working software over comprehensive documentation. This doesn’t mean ‘provide no documentation at all’ nor does it imply the developer must focus on producing code that won’t need maintaining down the road. Lest we forget Knuth’s valuable teachings on Literate Programming: “Instead of imagining that our main task is to instruct a computer what to do, let us concentrate rather on explaining to human beings what we want a computer to do.” (Donald Knuth. “Literate Programming (1984)” in Literate Programming. CSLI, 1992, pg. 99).
- Welcome changing requirements, value responding to change over following a plan, value customer collaboration over contract negotiation. These do not give either the development firm or the customer license to skip meetings intended to review current development capabilities, to collect as many requirements as possible, to create a plan for accommodating changes in technologies and priorities, and to set scope and expectations.

This is not to say Agile is broken or that Agile shouldn’t be adapted to fit each enterprise’s needs. _Au contraire_, I always advocate for choosing the right tools to solve a given problem. For instance, don’t use assembly language for complex UI design. Furthermore, each problem is unique and distinct. There is no “one size fits all” solution. Object-oriented design patterns are a great foundation but they may need to be adapted, depending on the specific problem being solved (keeping in mind that any adjustment should be in accordance with good object-oriented software design).

However, everyone must understand and properly execute the foundations of software development, regardless of the methodology, tools, and processes. Let’s discuss a bit more the impact of foregoing these principles when it comes to Enterprise Mobility.

### Requirements Gathering

Gathering requirements is not simply an act of “deciphering” what the customer wants but also a process of informing the client of things they might not be aware of and offering design-appropriate solutions for these cases.

Consider the scenario of a simple mobile enterprise application used to gather sensitive, personally identifiable employee information which will eventually be stored in the cloud. Capturing and storing text is a simple enough task for any software engineer. But without a strong background in handling personal data, the necessary security precautions regarding online storage may be ignored, or worse, the sensitive data may wind up being broadcast unencrypted across the internet, compromising the social security numbers of all employees.

### Framework Design

Of all aspects of software development, mobile applications for the Enterprise are the most prone to requirement changes. These can be as simple as an extra entry on an input screen or as complex as a complete backend overhaul. In either case, a few lines of code or an environment configuration change with a full round of testing can mean weeks, or even months (in the latter case), in Software and Quality Assurance expenses if the framework wasn’t properly designed in the first place.

I’m not here to evangelize on the principles for properly designing software frameworks, nor am I trying to teach good framework design in a few paragraphs. That would be impossible. No programmer is born knowing how to make software which is maintainable, scalable, extensible, et al. Nothing but experience, dedication, and eagerness to learn can afford a software engineer a glimpse into the fascinating world of framework-design theory.

When it comes to enterprise mobility, the backing of a team experienced in framework design along with the proper allocation of time and the facilitation of resources is paramount to avoid an out-of-control change-spiral—whether during development or years after the release.

### Unit Testing

Given the requirement-change proneness intrinsic to Enterprise mobile application development, unit testing becomes an inevitable consequence. Any and all changes—particularly those derived from shifts in requirements—must be proven to have not introduced undesired side effects. The early implementation of unit tests across the application will significantly improve end-product quality, as well as provide another tool for streamlining the identification of issues.

Yes, creating unit tests can add to the cost of development. However, this initial investment will undeniably pay huge dividends when an otherwise hard-to-track bug gets unveiled and is fixed in practically no time.

### Wrap-Up

Although software development involves many more practices than those mentioned above, the ones I focused on fit nicely together in a succession chain: the earlier stage gives way for the following stage’s natural execution. For instance, modeling all the (functional and non-functional) requirements towards a well-formed Application Public Interface makes the creation of unit tests a breeze. 
