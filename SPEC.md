# Hyperflow specification

Hyperflow is an agentic extension of hypermedia.

## Scope

This specification defines Hyperflow's concepts, their relationships, and
conceptual behavior. It gives web developers, web tool developers, and their
agents a shared basis for building and evaluating implementations. Technical
implementation and interface design are outside its scope.

Hyperflow remains a proposal. The definitions and behavior described here
establish its current meaning and are open to deliberate revision.

## The paradigm

Hyperflow encompasses working with material on a webpage through Markup and
Markup Notes, saving them, requesting agentic work, and using the resulting
webpages. The name refers to this whole paradigm.

The person selects the material and contributes the words attached to it.
An explicit request starts agentic work from that saved material and note.
The work produces a regular, complete webpage for the person to explore and
use. Selecting, saving, generation, and navigation are actions within
Hyperflow.

## Web material

Web material is the content a person encounters on a webpage. It can include
text, images, video, sound, and other hypermedia. A selection identifies the
material the person is working with: a passage, an image or part of an image,
a moment or interval in video or sound, or another identifiable part.

The selected material supplies the subject for the person's attached words.
Understanding those words depends on understanding what they refer to.
For example, “Explain this step” can concern a selected instruction in a
written guide or an action shown in a selected interval of video. The same
words refer to different material in each case.

The relationship between a selection and its surrounding material also
contributes meaning. A passage belongs to a document; a detail belongs to an
image; an interval belongs to a sequence. Selection identifies the subject
of the person's words within that setting.

## Markup

A **Markup** is the highlight on material a person selects. It identifies
the material to which the person's Markup Note is attached.

The selected material, its Markup, and its Markup Note have distinct roles.
In a highlighted paragraph, the paragraph supplies the material, the
highlight is the Markup, and the attached words are the Markup Note.
Highlighting an image region establishes the same relationship with visual
material.

### Saving a Markup

Saving retains the Markup and its Markup Note together. This keeps the
person's words associated with the material they selected. The saved Markup
and Markup Note can be inspected without requesting agentic work.

Saving does not start generation. The person separately requests work from
the saved material and note.

### Managing a Markup

A person can revise the attached Markup Note and save their changes. They
can also delete the Markup, removing its highlight and attached Markup Note
without deleting the underlying web material.

These actions concern what the person has saved. Inspecting, revising,
saving, or deleting a Markup does not by itself request generation.

## Markup Note

A **Markup Note** is the person's written note attached to a Markup. It
expresses what the person has to say or asks to have done in relation to the
selected material. It can contain a question, an observation, or a direction
for agentic work.

The attachment connects the words to their subject. A Markup Note can
therefore refer to the selected material without restating it. “Explain
this for a beginner” takes its subject from the material identified by the
Markup.

The person's words also distinguish different uses of the same material.
In one illustrative use of a passage, the Markup Note might say “Explain
this for a beginner.” In another use of that passage, it might say “Challenge
this argument.” Both concern the same text, but they ask for different work.
The selected material and the Markup Note contribute together to what
generation addresses.

## Generation

Generation is the agentic work started by a person's explicit request using
the saved material and Markup Note. The material provides the subject, and
the person's words guide the work in relation to it.

### The generation request

The request initiates an agentic workflow. It is separate from selecting
material, writing a Markup Note, and saving. A person who saves without
requesting generation has retained their Markup and Markup Note without
starting that work.

### Agentic work

The agent works with the selected material in light of the Markup Note to
produce a complete webpage. The note might ask for an explanation, a
comparison, an adaptation, or other work concerning that material.

For example, a person could select a configuration example in documentation
and attach the Markup Note “Adapt this for an environment with two
application servers.” A generation request from that saved material and
note could produce a webpage explaining an adapted configuration.

## Generated webpages

A generated webpage is the regular, complete webpage produced by the
agentic work. It gives the result a form the person can read, explore, and
use. “Generated” identifies how the webpage came into being; the page
remains part of the web.

The page's content serves the work requested from the selected material and
Markup Note. It could be an explanation, a comparison, a plan, a tool, or
another useful webpage. These illustrate possible results within the
paradigm.

### Continued browsing

The resulting webpage can itself provide material for a Markup and Markup
Note. The person can select something there, attach their words, save them,
and request further work. The same concepts apply when the selected
material is on a page produced through Hyperflow.

Ordinary links can also lead onward. Links and Markups can coexist within
the same webpage and the same browsing experience.

---

*This text is dedicated to the public domain (CC0 1.0). Hyperflow™ is
claimed as a trademark. · hyperflow.org*
