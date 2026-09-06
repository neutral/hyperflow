<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://hyperflow.org/assets/logo-dark.svg">
    <img src="https://hyperflow.org/assets/logo.svg" alt="" width="96">
  </picture>
</p>

# Hyperflow

Hyperflow is an agentic extension of hypermedia.

A person selects material on a webpage and attaches their own words to it.
The highlight is the **Markup**; the attached words are its **Markup Note**.
Saving retains them together. A separate, explicit generation request starts
agentic work from the saved material and note, producing a regular, complete
webpage for the person to explore and use.

The material can be text, an image region, a moment in a video, or another
part of a webpage. A Markup Note can ask a question, make an observation,
or give direction for work. The person can inspect a saved Markup, revise
its Markup Note, or delete the Markup without starting generation.

## An example

On a documentation page, a person highlights a configuration example and
adds the Markup Note “Adapt this for an environment with two application
servers.” They save it, then request generation. The agent could produce a
webpage explaining an adapted configuration.

That page gives the person something to read, inspect, and work from. Its
material can become the subject of another Markup and Markup Note. Ordinary
links can also lead onward; both can coexist on the same webpage.

## Build from the specification

[Read SPEC.md](SPEC.md) for the concepts, their relationships, and how they
behave. Hyperflow remains a proposal, open to revision through building
and use.

The specification is for web developers, web tool developers, and their
coding agents. You can use it directly when building support into your own
webpages or creating reusable tools. It establishes shared meaning while
leaving interface design and technical implementation to you.

Feedback from implementations helps refine the proposal. Open an issue in
this repository with the task you tried, how the concepts applied, and
where the specification was unclear.

## License and name

The text here is dedicated to the public domain under
[CC0 1.0](LICENSE.md). Hyperflow™ is a trademark: use the name
freely to describe conforming implementations; don't use it to brand
something that isn't one, or to imply endorsement.

[hyperflow.org](https://hyperflow.org) · info@hyperflow.org
