# Prompt used for the initial elicitation pass

This is the instruction given to the language model for the first requirements pass. The result is [the product backlog](requirements-backlog.md), with the same items in tagged form in [requirements.json](requirements.json).

---

You are helping with an initial requirements elicitation pass for a one-semester software engineering course (CEN4020). The author chose Scrum over Kanban for the term. Produce a product backlog, not a design and not sprint commitments.

## Problem, in the author's words

> In my DevOps course I learnt about the two methods and delved into projects assigning characteristics of both, in my opinion SCRUM is a more agile, day-to-day setting that allows for more dynamic, and therefore, "faulty" by nature project, which I understand as a good thing at first. In my view Kanban is too methodical, to the point where tasks can just feel isolated and not realize the clashes until it's already too late.
>
> One of the issues I've encountered with most major streaming services is local availability, having tried Spotify, Deezer and apple music, all 3 fall short when your catalogue is too large, and locally saving those files will offer a better experience 100% of the times; usually lookup times are way too long on all of them when your library exceeds even 3K songs. Don't know exactly yet what the problem i want to work with is, but for sure something along these lines.

The professor asked that the project stay somewhat reasonable for one term.

## What to produce

Turn that answer into a backlog for a desktop application. Name the product. Make a scoping choice where the answer is still open, and write the choice down as requirements so it can be challenged later.

The product is a local music library: folders of files the user already has, a catalogue that stays fast past a few thousand tracks, and playback that does not need a streaming account. Do not specify a streaming service, a downloader, or DRM removal.

Separate what the author actually said from what you inferred. Record assumptions and open questions instead of inventing answers for them.

## Metadata on every requirement

- id
- title
- type: functional, non-functional, or constraint
- epic
- priority: must, should, could, or wont, using MoSCoW for this term
- status: proposed
- confidence: high, medium, or low
- persona
- source: problem-statement, derived, domain, or scope
- tags
- depends_on: ids of requirements that must be acceptable before this one can be accepted
- a user story for functional items, or a requirement statement for non-functional items and constraints
- acceptance criteria that a later test could check
- notes when the item is an assumption, a risk, or a proposed number rather than a measured one

## Dependency rules

- Identify dependencies in both directions in the readable backlog (depends on, and blocks).
- Keep the graph acyclic.
- A Must requirement may depend only on other Must requirements.
- Won't items are scope boundaries. Give them no dependents.

## Also include

- stakeholders and personas
- a design point for any performance target, tied to the author's "about 3,000 tracks" experience, and label the numbers as proposed
- an explicit first-release slice (the Must set) and a suggested order for pulling that slice into sprints
- a machine-readable copy of the same items so the tags and dependencies are unambiguous
