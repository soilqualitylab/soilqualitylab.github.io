---
layout: post
title:  "Semantic Versioning and Conventional Commit Discipline"
subtitle:  "Try to communicate better with your future"
date:   2023-03-01 4:30:00
categories: template
---


# Questions the FUTURE you is going to ask the current you

Constantly be flanking yourself and the old habits of being yourself. ***Clinging to the old you is what sabotages the new, improved future you.***

PRACTICE improving the habits of being yourself by improving your [commit discipline](https://zulip.readthedocs.io/en/latest/contributing/commit-discipline.html) and generally becoming more knowledgable and practiced in things like the art of [GitOps](https://about.gitlab.com/topics/gitops/) and generally aware of [how/why code review tools have been evolving in the last decade or two](https://www.gerritcodereview.com/about.html) ... 

You will want to minimalize what goes into an individual commit [which generally means maximizing the number of separate commits] into tight, well-disciplined atomic commits *without overdoing your minimalistic tendencies.* Frankly, this is a bit of an art one learns through a lot of practice ... a commit with [a solid commit message](https://github.com/zulip/zulip/commit/084dd216f017c32e15c1b13469bcbc928cd0bce9) should stand alone as a coherent thought for other skilled collaborators who know Git well enough to [follow git histories](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History) but were not along with you at the time of your original thinking when the commit was made. You will want to really internalize and ***USE*** [semantic versioning](https://semver.org/) [conventional commit](https://www.conventionalcommits.org/en/v1.0.0/#specification) best practices so that the [automation toolboxes](https://github.com/cocogitto/cocogitto) you use help to develop cleaner, tighter, more readable commit histories, ie *it's about the* ***maintainability***, *stupid!* 

# Embrace the microdiscipline of conventional commits

Conventional commits are an exercise in being more mindful and respectful of your fellow professionals as well as your future self.

Extreme ownership means that YOU have to bring and elevate your discipline of being more mindful ... you PRACTICE mindfulness discipline by trying to anticipate the questions or searches that the future you will ask.

Making your shit FINDABLE is one element of embracing ASYNCHRONICITY.  You must take charge of your own skillset, habits, disciplines so that are able to collaborate with the future you ... OR so that you are better able to communicate with anyone, anywhere, anytime. 

If it was not already painfully obvious BEFORE, embracing asynchronicity makes it even more imperative that you **manage your own time** and, above all, ***be much more focused on YOUR WHY***. *Stop settling for masters who demand that you kowtow to their agenda.*

# All genuinely useful code ends up being reviewed, forked, completely changed by someone else

***... or else, without this review/forking process, code just becomes dead code, perhaps favorite pet of some old geezer, but something that just sits on those hard-drive which end up at Recycling Center ... so the code is never used or heard from again.***

The most useful code will inspire extension and forking. More ideas are better than fewer ideas; often, specific oddball ideas are a much better fit for different situations than they are for the general use case. Thus, Git works best when developers anticipate future, but unforeseeable riffing, diffing, forking, play and improvisation. To make it possible to make the most of the proliferation of ideas, we should try to make sure that one commit should corresponds to one functional change, as is required for the sortability of things like:

[git revert](https://git-scm.com/docs/git-revert)

[git cherry-pick](https://git-scm.com/docs/git-cherry-pick)

[git bisect](https://git-scm.com/docs/git-bisect)