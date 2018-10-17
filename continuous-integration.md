<!-- TITLE: Continuous Integration -->
<!-- SUBTITLE: A quick summary of Continuous Integration -->

# Continuous integration
[video](https://www.youtube.com/watch?v=xSv_m3KhUO8){.youtube}


Software development
Core activities
Processes Requirements Design Engineering Construction Testing Debugging Deployment Maintenance
Paradigms and models
Agile Cleanroom Incremental Prototyping Spiral V model Waterfall
Methodologies and frameworks
ASD DevOps DAD DSDM FDD IID Kanban Lean SD LeSS MDD MSF PSP RAD RUP SAFe Scrum SEMAT TSP UP XP
Supporting disciplines
Configuration management Documentation Software quality assurance (SQA) Project management User experience
Practices
ATDD BDD CCO CI CD DDD PP Stand-up TDD
Tools
Compiler Debugger Profiler GUI designer Modeling IDE Build automation Release automation Infrastructure as Code Testing
Standards and Bodies of Knowledge
BABOK CMMI IEEE standards ISO 9001 ISO/IEC standards PMBOK SWEBOK ITIL
Glossaries
Artificial intelligence Computer science Electrical and electronics engineering
vte
In software engineering, continuous integration (CI) is the practice of merging all developer working copies to a shared mainline several times a day.[1] Grady Booch first proposed the term CI in his 1991 method,[2] although he did not advocate integrating several times a day. Extreme programming (XP) adopted the concept of CI and did advocate integrating more than once per day – perhaps as many as tens of times per day.[3]


Contents
1	Rationale
2	Workflow
3	History
4	Common practices
4.1	Maintain a code repository
4.2	Automate the build
4.3	Make the build self-testing
4.4	Everyone commits to the baseline every day
4.5	Every commit (to baseline) should be built
4.6	Keep the build fast
4.7	Test in a clone of the production environment
4.8	Make it easy to get the latest deliverables
4.9	Everyone can see the results of the latest build
4.10	Automate deployment
5	Costs and benefits
6	See also
7	References
8	Further reading
9	External links
Rationale
The main aim of CI is to prevent integration problems, referred to as "integration hell" in early descriptions of XP. CI is not universally accepted as an improvement over frequent integration, so it is important to distinguish between the two as there is disagreement about the virtues of each.[citation needed]

In XP, CI was intended to be used in combination with automated unit tests written through the practices of test-driven development. Initially this was conceived of as running and passing all unit tests in the developer's local environment before committing to the mainline. This helps avoid one developer's work-in-progress breaking another developer's copy. Where necessary, partially complete features can be disabled before committing, using feature toggles for instance.

Later elaborations of the concept introduced build servers, which automatically ran the unit tests periodically or even after every commit and reported the results to the developers. The use of build servers (not necessarily running unit tests) had already been practised by some teams outside the XP community. Nowadays, many organisations have adopted CI without adopting all of XP.

In addition to automated unit tests, organisations using CI typically use a build server to implement continuous processes of applying quality control in general — small pieces of effort, applied frequently. In addition to running the unit and integration tests, such processes run additional static and dynamic tests, measure and profile performance, extract and format documentation from the source code and facilitate manual QA processes. This continuous application of quality control aims to improve the quality of software, and to reduce the time taken to deliver it, by replacing the traditional practice of applying quality control after completing all development. This is very similar to the original idea of integrating more frequently to make integration easier, only applied to QA processes.

In the same vein, the practice of continuous delivery further extends CI by making sure the software checked in on the mainline is always in a state that can be deployed to users and makes the actual deployment process very rapid.

Workflow
When embarking on a change, a developer takes a copy of the current code base on which to work. As other developers submit changed code to the source code repository, this copy gradually ceases to reflect the repository code. Not only can the existing code base change, but new code can be added as well as new libraries, and other resources that create dependencies, and potential conflicts.

The longer a branch of code remains checked out, the greater the risk of multiple integration conflicts and failures when the developer branch is reintegrated into the main line. When developers submit code to the repository they must first update their code to reflect the changes in the repository since they took their copy. The more changes the repository contains, the more work developers must do before submitting their own changes.

Eventually, the repository may become so different from the developers' baselines that they enter what is sometimes referred to as "merge hell", or "integration hell",[4] where the time it takes to integrate exceeds the time it took to make their original changes.

Continuous integration involves integrating early and often, so as to avoid the pitfalls of "integration hell". The practice aims to reduce rework and thus reduce cost and time.[5]

A complementary practice to CI is that before submitting work, each programmer must do a complete build and run (and pass) all unit tests. Integration tests are usually run automatically on a CI server when it detects a new commit.

History
[icon]	
This section needs expansion. You can help by adding to it. (August 2014)
The earliest known work on continuous integration was the Infuse environment developed by G.E. Kaiser, D.E. Perry and W.M. Schell.[6]

In 1994, Grady Booch used the phrase continuous integration in Object-Oriented Analysis and Design with Applications (2nd edition)[7] to explain how, when developing using micro processes, "internal releases represent a sort of continuous integration of the system, and exist to force closure of the micro process."

In 1997, Kent Beck and Ron Jeffries invented Extreme Programming (XP) while on the Chrysler Comprehensive Compensation System project, including continuous integration.[8] Beck published about continuous integration in 1998, emphasising the importance of face-to-face communication over technological support.[9] In 1999, Beck elaborated more in his first full book on Extreme Programming.[10] CruiseControl, one of the first open-source CI tools,[11] was released in 2001.

Common practices

This section contains instructions, advice, or how-to content. The purpose of Wikipedia is to present facts, not to train. Please help improve this article either by rewriting the how-to content or by moving it to Wikiversity, Wikibooks or Wikivoyage. (May 2015)
This section lists best practices suggested by various authors on how to achieve continuous integration, and how to automate this practice. Build automation is a best practice itself.[12][13]

Continuous integration – the practice of frequently integrating one's new or changed code with the existing code repository – should occur frequently enough that no intervening window remains between commit and build, and such that no errors can arise without developers noticing them and correcting them immediately.[14] Normal practice is to trigger these builds by every commit to a repository, rather than a periodically scheduled build. The practicalities of doing this in a multi-developer environment of rapid commits are such that it is usual to trigger a short time after each commit, then to start a build when either this timer expires, or after a rather longer interval since the last build. Note that since each new commit resets the timer used for the short time trigger, this is the same technique used in many button debouncing algorithms [ex:[15]]. In this way the commit events are "debounced" to prevent unnecessary builds between a series of rapid-fire commits. Many automated tools offer this scheduling automatically.

Another factor is the need for a version control system that supports atomic commits, i.e. all of a developer's changes may be seen as a single commit operation. There is no point in trying to build from only half of the changed files.

To achieve these objectives, continuous integration relies on the following principles.

Maintain a code repository
Main article: Version control
This practice advocates the use of a revision control system for the project's source code. All artifacts required to build the project should be placed in the repository. In this practice and in the revision control community, the convention is that the system should be buildable from a fresh checkout and not require additional dependencies. Extreme Programming advocate Martin Fowler also mentions that where branching is supported by tools, its use should be minimised.[14] Instead, it is preferred for changes to be integrated rather than for multiple versions of the software to be maintained simultaneously. The mainline (or trunk) should be the place for the working version of the software.

Automate the build
Main article: Build automation
A single command should have the capability of building the system. Many build tools, such as make, have existed for many years. Other more recent tools are frequently used in continuous integration environments. Automation of the build should include automating the integration, which often includes deployment into a production-like environment. In many cases, the build script not only compiles binaries, but also generates documentation, website pages, statistics and distribution media (such as Debian DEB, Red Hat RPM or Windows MSI files).

Make the build self-testing
Once the code is built, all tests should run to confirm that it behaves as the developers expect it to behave.[16]

Everyone commits to the baseline every day
By committing regularly, every committer can reduce the number of conflicting changes. Checking in a week's worth of work runs the risk of conflicting with other features and can be very difficult to resolve. Early, small conflicts in an area of the system cause team members to communicate about the change they are making.[1] Committing all changes at least once a day (once per feature built) is generally considered part of the definition of Continuous Integration. In addition performing a nightly build is generally recommended.[citation needed] These are lower bounds; the typical frequency is expected to be much higher.

Every commit (to baseline) should be built
The system should build commits to the current working version to verify that they integrate correctly. A common practice is to use Automated Continuous Integration, although this may be done manually. For many[who?], continuous integration is synonymous with using Automated Continuous Integration where a continuous integration server or daemon monitors the revision control system for changes, then automatically runs the build process.

Keep the build fast
The build needs to complete rapidly, so that if there is a problem with integration, it is quickly identified.

Test in a clone of the production environment
Main article: Test environment
Having a test environment can lead to failures in tested systems when they deploy in the production environment because the production environment may differ from the test environment in a significant way. However, building a replica of a production environment is cost prohibitive. Instead, the test environment, or a separate pre-production environment ("staging") should be built to be a scalable version of the actual production environment to both alleviate costs while maintaining technology stack composition and nuances. Within these test environments, service virtualization is commonly used to obtain on-demand access to dependencies (e.g., APIs, third-party applications, services, mainframes, etc.) that are beyond the team's control, still evolving, or too complex to configure in a virtual test lab.

Make it easy to get the latest deliverables
Making builds readily available to stakeholders and testers can reduce the amount of rework necessary when rebuilding a feature that doesn't meet requirements. Additionally, early testing reduces the chances that defects survive until deployment. Finding errors earlier also, in some cases, reduces the amount of work necessary to resolve them.

All programmers should start the day by updating the project from the repository. That way, they will all stay up to date.

Everyone can see the results of the latest build
It should be easy to find out whether the build breaks and, if so, who made the relevant change and what that change was.

Automate deployment
Most CI systems allow the running of scripts after a build finishes. In most situations, it is possible to write a script to deploy the application to a live test server that everyone can look at. A further advance in this way of thinking is continuous deployment, which calls for the software to be deployed directly into production, often with additional automation to prevent defects or regressions.[17][18]
