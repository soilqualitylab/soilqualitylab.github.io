---
layout: page
title: GitRxiv
permalink: /GitRxiv/
---

# Not Just a Polyglot, but a PolyGit

You already know why you need to be a polyglot, but you also really need to be PolyGIT ... able to think in Git as a native and aware of *different ways to cook the ol' egg* in Git ... you want to stay positive, yet critically review an action ... even though you might use one way to accomplish a certain kind of objective 99% of the time -- not everybody you work with is going to have your same workflow. You really need to be able to understand their workflow from the inside, maybe to offer them a better way OR, maybe they have found a better way for you to adapt. 

Being a PolyGit is about being able to get inside the thinking and *see what someone else did there* rather than either just accepting it with an eye roll or just rejecting it out of hand.

The reason why you need to be a PolyGit is that in asynchronous workflows, **we don't rely upon meetings -- INSTEAD we rely on genuinely, helpfully, empathetically, constructively OVERCOMMUNICATING.**

Asynch workflows are best built on Git ... if you want to be part of these workflows, you **have to be** a PolyGit in order to competently OVERCOMMUNICATE in Git-based code reviews and all Git-based communications.

## Git SuperFluency for Asynchronous Overcommunication

The absolute minimum PREREQUISITE for any serious attempt at engineering an asynchronous workflow is going to be an ongoing commitment to going back to the [basics of Git, especially Git branches](https://github.com/git-guides#create-a-branch) and engaging in the neverending improvement in your fluency in [Git commands](https://git-scm.com/docs/git) and that fluency will have to be grounded in a firm understanding of [Git concepts](https://git-scm.com/docs/user-manual#git-concepts).

Although we genuinely love tools like [GitLens, because of how visual tools help illuminate knowledge with a repository](https://www.gitkraken.com/gitlens?utm_source=gitlens-extension&utm_medium=in-app-links&utm_campaign=gitlens-logo-links),we do have a strong preference for being aware of [Git CLI Commands](https://git-scm.com/docs/git), rather than just trusting the graphical user interfaces, particularly Windows and Node.JS interfaces, because ubiquitous easy to use [and never second-guess] attracts evil, but we are not terribly dogmatic about this -- the main point is that just that you even if your don't use the CLI, you will inevitably still need to understand some things about what is happening *under the hood*.

### Git Concepts

There's not really an substitute for an in-depth, intuitive understanding of [Git concepts](https://git-scm.com/docs/user-manual#git-concepts), why you use Git, and how Git works.  

[Understanding commit history](https://git-scm.com/docs/user-manual#understanding-commits) is based on a solid foundation of really understand the [object storage format](https://git-scm.com/book/en/v2/Git-Internals-Git-Objects) and relationships in the git internal architecture of the four different types of objects: [commit object](https://git-scm.com/docs/user-manual#def_commit_object) links a physical state of a tree with a description of how we got there and why, [tree object](https://git-scm.com/docs/user-manual#def_tree_object) object contains a list of entries, each with a mode, object type, SHA-1 name, and name, sorted by name, [tag objects](https://git-scm.com/docs/user-manual#def_tag_object) are more focused on versioning, findability, and reproducibility but they can be used to incorporate a degree of trust and authenticity into overall system; tags contain an object, object type, tag name, the name of the person ("tagger") who created the tag, and a message, which may contain a signature and [blob objects](https://git-scm.com/docs/user-manual#def_blob_object) nothing but a binary blob defined entirely by its file data; of course, file data is the basis of what you are working on under version control system, but don’t refer to anything else or have attributes of any kind.  

### Git Butler for Multitasking Across Branches

Multitasking across related branches to review/try out/revise code is almost necessary capability for anyone with others in an asynchronous workflow. There are different ways to do this *manually* using [git add -p](https://g.co/gemini/share/9bbd292b1664) and [git rebase -i](https://g.co/gemini/share/dd723bdb9d05) ... but using a tool like [GitButler](https://gitbutler.com/) is a more flexible, more efficient way to multitask across branches.

When multitasking across related branches and reviewing code with a distributed team using Git repositories, there are several STARDARD [rules of communication](https://ben.balter.com/2014/11/06/rules-of-communicating-at-github/) to require developers on the team to follow:

1. Efficient code review [and future code maintainability] is built on a foundation of standard, clean [conventional commits](https://www.conventionalcommits.org/en/v1.0.0/#summary) ... for example: 

        Add search functionality to user dashboard
        - Implement search bar in the user dashboard
        - Allow users to search for specific records by name or ID
        - Display search results in a paginated table
        
        Closes #123

2. Use descriptive, clear branch names that identify the purpose, feature, bug fix, or task reference. Keep branches focused on separate branches for each distinct feature, bug fix, or task. A feature branch workflow where each feature or task is developed in a separate branch and merged back into the main branch after review and approval promotes isolation of issues, coherent parallel development, and clear integration points.

3. Regularly push changes to the remote repository frequently to communicate progress and get feedback from team members; this enables collaboration and provides a backup of your work. 

4. Keep feature branches up to date by regularly merge the latest changes from the main branch into your feature branches. This helps minimize merge conflicts and ensures that changes in feature branches are compatible with the **latest** main branch codebase.

5. Overcommunicate with BETTER (ie, write it, let it sit, revise it) descriptions in pull [or merge] requests the clearly, concisely describe the problem being solved and the relevant context why it matters to the code, ie not "I was working on X, so I got to thinking about Y, then I worked how X and Y are related by Z which is the inverse A, so here's A". Utilize [pull requests on GitHub](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests) OR [merge on GitLab](https://docs.gitlab.com/ee/user/project/merge_requests/) requests to propose changes, to initiate code review and reinforce issue-driven development practices by centralizing the location comments related to the proposed change before merging the feature branch into the main branch. 

6. Beyond just communication, foster collaboration among team members by continually levelling up mastery and leveraging the different tools provided by Git hosting platforms (e.g., GitHub, GitLab) and to the greatest degree possible standardize on toolchain components. There probably should be a standard ***team*** integrated development environment that everyone uses. Leveraging the standard IDE helps build a shared proficency in communicating through approval workflows and branch related comments, but this also means that there must be a standard, designated discussion board for more general suggestions or non-branch related commentary. 

7. Require all developers on the team to implement standard automated testing and continuous integration (CI) processes to catch potential issues as early as possible and better ensure that the codebase remains stable. These tests and checks have to be run automatically, ideally before changes are pushed to the repository.

8. Continually work to set expectations for the individuals on team to prioritize reviewing code to drive more frequent, smaller and better review of pull requests.

9. Document and share the team's agreed-upon best practices, coding conventions, and workflow guidelines. Ensure that all team members are familiar with and follow these practices consistently, by referencing the best practices documents.

10. Avoid ROUTINE meetings. Most work should be done asynchronously ... accordingly to people's lives ... not tyrannically hi-jacked by the lowest-common denominator demand for a meeting.  It is permissible even necessary at times to use communication channels like chat or zoom video conferencing to discuss complex changes, clarify doubts, or resolve thornier conflicts -- but recognize that relying on **routine** meetings is generally a sign of a broken commitment to standardization and overcommunication.

Remember, effective multitasking and code review processes require discipline, communication, and collaboration among team members. By following these best practices and adapting them to your team's specific needs, you can streamline your workflow and maintain a high-quality codebase while working on multiple related branches.

In using just Git alone, it is preferable or pretty much necessary when working with others, that you create your desired branches ahead of time, but when using a tool like [GitButler client](https://gitbutler.com/), the client helps you to keep track of uncommitted changes by grouping those changes into GitButler's own ***virtual branch*** layer ***on top of*** Git. Whenever you are happy with the contents of a virtual branch, you can push it to a remote. GitButler makes sure that the state of other virtual branches is kept separate from *normal* Git branches. *Normal* Git branches are separate universes and switching between them is **a full context switch**. 

[GitButler](https://gitbutler.com/) allows you to work with multiple virtual branches in parallel in the same working directory. This effectively means having the content of multiple branches available at the same time. GitButler is aware of changes before they are committed. This allows it to keep a record of which virtual branch each individual diff belongs to. Effectively, this means that you can separate out individual branches with their content at any time to push them to a remote or to unapply them from your working directory. 

For an asynchronous workflow, we ***strongly*** prefer [GitButler](https://gitbutler.com/) ... an [open source Git client](https://github.com/gitbutlerapp/gitbutler) for working on multiple branches at the same time. It allows you to quickly organize file changes into separate branches while still having them applied to your working directory. You can then push branches individually to your remote, or directly create pull requests. 

### Tauri 

Strictly speaking, you would not absolutely NEED to use [GitButler](https://gitbutler.com/), ***HOWEVER*** the reason that we strongly recommend using GitButler itself and understanding some things about the code of the [open source Git client](https://github.com/gitbutlerapp/gitbutler) is all about understanding [why Tauri was built for security-focused, privacy-respecting, and environmentally-conscious software engineering community](https://tauri.app/v1/references/architecture/) and that extends to Tauri-related dev things like [how Tauri was used to build Rust code and debug GitButler in VSCode](https://blog.gitbutler.com/debugging-tauri-in-vs-code/).

[Tauri](https://github.com/tauri-apps/awesome-tauri) is popular application toolkit written in Rust that allows for making tiny, blazingly fast Webview OS applications, such as the [GitButler client](https://github.com/tauri-apps/awesome-tauri?tab=readme-ov-file#developer-tools); Tauri is not some sort of VM that allows code to run efficiently and securely in web browsers like [WASM](https://rustwasm.github.io/docs/book/) or ***rust****ified* spin on [Chromium V8 JavaScript Engine](https://github.com/v8/v8) or virtualized environment OR a lightweight kernel wrapper OR even a virtual machine monitor such as [Cloud Hypervisor](https://github.com/cloud-hypervisor/cloud-hypervisor) or [Firecracker](https://github.com/firecracker-microvm/firecracker). 

Instead, [Tauri's architecture](https://tauri.app/v1/references/architecture/) relies on [WRY](https://github.com/tauri-apps/wry) and [TAO](https://github.com/tauri-apps/tao) to do the heavy lifting that an application does in making system calls directly to the OS. [WRY](https://github.com/tauri-apps/wry) is a cross-platform WebView rendering library in Rust which is the cross-platform abstract layer responsible to determining which webview is used and how interactions are made. The [TAO](https://github.com/tauri-apps/tao) of cross-platform windowing [for all major desktop and mobile platforms] window creation library that supports menu bars and system trays. 

### Rust

Strictly speaking, you would not absolutely NEED to use the [Tauri architecture](https://github.com/tauri-apps/tauri/blob/dev/ARCHITECTURE.md) to build and improve toolchain apps for ASYNCHRONOUS workflows ... obviously, a [statically-typed languages like Rust that allow for compiler-checked constraints on the data and its behavior](https://stackoverflow.blog/2020/01/20/what-is-rust-and-why-is-it-so-popular/) will alleviating cognitive overhead and misunderstandings, but there's a learning curve, in spite of Rust's thriving and growing ecosystem, because of Rust's opinionated strong type system and emphasis on memory safety. It's ORDINARY to get errors when compiling your code; even if the error messages will be clear and actionable [after you have internalized Rust's way of doing things and Rust's idioms](https://doc.rust-lang.org/book/ch17-01-what-is-oo.html), you should expect to be a bit frustrated at first. Tiny, secure, blazingly faster applications that really fly ... rather than just more error messages at compile time ... can be a reality, if one can learn [and steal the best ideas] from large development communities. 

Participating in a development community, like Tauri's, is going to be a shortcut for [doing Rust well for DevOps tooling](https://doc.rust-lang.org/book/ch00-00-introduction.html). It's generally better to follow the forks and stars on Github to see which approach has the deepest, broadest community support ... unless, you really have special insight on what would make the architecture more secure, more reliable, and much faster, it's tough to argue with thousands of recent forks UNLESS you have something new that picking more thousands of forks. Rust language, itself, illustrates the necessity of paying attention to which direction the forks are moving in ... there are [an almost infinite number of computer languages that people have proposed](https://en.wikipedia.org/wiki/Programming_language_theory), but it is COMMUNITY of developers writing code in that language that make the language.

The reason to use a somewhat established application toolkit like Tauri is that most of pitfalls are taken out of your way and the [Tauri community](https://github.com/tauri-apps) is **very active** (2200 forks on GitHub) open source development community that is constantly improving the toolkit ... of course, it's a good idea to [stay current with reading on new developments in Rust](https://readrust.net/), but [building UIs in Rust UI in Rust is difficult](https://www.warp.dev/blog/why-is-building-a-ui-in-rust-so-hard), ie, if it were easy, Rust framework proliferation would be as rampant as it was with JavaScript. If something better than Tauri comes along, [like maybe a new spin on **Warp**](https://github.com/warpdotdev/Warp), or something else using [Iced, the cross-platform GUI library for Rust](https://github.com/iced-rs/iced), inspired by [Elm-Lang](https://guide.elm-lang.org/), a [purely functional language](https://en.wikipedia.org/wiki/Purely_functional_programming) that compiles to JavaScript ... whether something better than Tauri comes along or not, you will still want to [stay current with reading on new developments in Rust](https://readrust.net/).

A developer must first [learn something about Rust](https://doc.rust-lang.org/book/) and then install the prerequisite toolchains for creating a Tauri app and then dive in. At the very least this will entail [installing rust](https://doc.rust-lang.org/book/ch01-01-installation.html) & [cargo](https://doc.rust-lang.org/book/ch01-03-hello-cargo.html), and most likely also a modern version of node.js and potentially another package manager. Some platforms may also require other tooling and libraries, but this has been documented carefully in the respective platform docs.