# Hyperflow — the specification

v0.3.0

## Short version

A Hyperflow is an ordered sequence of Panels. Think of each Panel as a web
page with one job. Behind every Panel there's a Shadow Context — the
Hyperflow's notes about that Panel, kept up to date. When you request the
next Panel, the Request carries what you actually marked, not the whole
Hyperflow; if the agent needs more, the shadow contexts are right there. A
successful Request adds exactly one Panel to the end, and a failed one
changes nothing at all. A Panel gets generated once, then rendered and refreshed like any page you've ever shipped — the
structure's fixed, the data stays live. And a Hyperflow is meant to be
kept: pinned, reopened, picked up next week, handed to a teammate.

## Glossary

**Hyperflow** — one ordered trail of Panels: you pin a Hyperflow,
reopen it, hand it to someone. The word also names the model as
a whole, the way "hypertext" named both the medium and the material, and
context tells the two apart.

**Panel** — a page with one job, rendered by your app. It can be a
document with media and widgets in it or fully interactive. A Panel at
the end of a
Hyperflow stands on everything before it, through the shadow contexts. And inside a Panel, a hyperlink is still
just a hyperlink: clicking one is normal web navigation, not a Request.
Routing normal navigation through generation would just rebuild the
browser, slowly.

**Request** — how a Hyperflow grows. Every Request starts from marked
material, and there are two ways to mark: a Highlight, which someone set
up ahead of time (marked text or media with a prompt behind it), and an
Annotation, which the user makes on the spot (select something, attach a
thought, ask). Either way the Request carries what was marked and said,
plus which Panel it extends. The Request supplies the subject, and the
Shadow Context supplies the situation. How highlights and annotations look
in your app is your call.

**Render** — the current presentation of a Panel, with its references
resolved against live sources. Anything that will go stale is stored as a
reference at generation and looked up at render time.

**Refresh** — resolving those references again and presenting the Panel
again. It's the same gesture as reloading a page, with the same guarantee:
the page you had, with current data. Panels can also update themselves
internally — polling, streams, whatever your pages already do — and none
of that touches the Hyperflow.

**Shadow Context** — the notes kept behind each Panel: what it is, what
it's showing right now, what its references currently resolve to. It
updates when its Panel renders or refreshes. When a new Panel is being
generated, every Shadow Context in the Hyperflow is available; the agent
takes what it needs, and the new Panel cites what was used. Private drafts
and annotations nobody submitted stay out by default.

**Panel Engine** — the thing that satisfies Requests: a Request goes in, a
Render comes back. Caching, app data, templates, agents, reference
resolution, shadow upkeep — all of that lives behind this boundary, and
none of it is prescribed here.

## Rules

These rules are what make something a Hyperflow.

### One ordered sequence

A Hyperflow is one sequence, in order. It can be a horizontal row on a
desktop and a stack of sheets on a phone — layout is yours, but membership
and order aren't. And it's the actual Panels too, not a strip of
thumbnails standing in for them.

Why so strict? Because the order is the explanation. Branch it into a
canvas and arranging things becomes the user's job again, and the
Hyperflow stops telling the story of how the inquiry went.

### One successor, or nothing

If a Request works, exactly one Panel is added at the end, and it's a real
page — links work, controls work, refresh shows current data, and you can
mark it and continue from it like anything else in the Hyperflow. If a
Request fails or gets abandoned, nothing changes: no spinner in the
sequence, no error card, no half-rendered stub that fills in later. Work
in progress lives outside the Hyperflow until it's done.

This is the rule that keeps a Hyperflow a record.

### The Hyperflow is not the prompt

Panels are for the user. What the model gets is the Request — the marked
material and what the user said — plus whatever it deliberately pulls from
the Shadow Contexts, and the new Panel cites what it used. Nothing enters
the prompt just because it was on screen.

The lazy version is pasting the whole Hyperflow in. Do that and you've
rebuilt ambient chat: answers grounded in everything, citing nothing, and
nobody can tell where any claim came from.

### An effect is not a step

Controls on a Panel can do anything your app allows — read, write, kick
off a job. None of it moves the Hyperflow, which grows only when someone
asks for the next Panel.

| What happened                         | What the Hyperflow does |
| ------------------------------------- | ----------------------- |
| Something updated inside a Panel      | Nothing                 |
| A backend read, write, or action ran  | Nothing                 |
| A Request succeeded                   | Adds exactly one Panel  |
| A Request failed                      | Nothing                 |

## Smallest real version

A list of panels in client state
and one function that requests the next one: append exactly one on
success, change nothing on failure, keep a note behind each panel for its
shadow context, resolve references at render time. That keeps all four
rules. And a Panel can be as humble as a block of markdown with a list of
references — "a real page" is about the role it plays in the Hyperflow.

Four quick checks to know you've got one:

- Abandon a request mid-flight and let it resolve late anyway. The
  Hyperflow is unchanged.
- Scroll back three panels. Each one still works — links click, refresh
  shows current data.
- Press a control that does something in the backend. The Hyperflow
  didn't move.
- Look at what was actually sent to the model and what came back. Marked
  material and drawn shadow context went in, a page that cites its inputs
  came out, and the Hyperflow itself appears nowhere in the prompt.

## Break the rest

Deliberately not prescribed: the shape of Requests and Renders, how Panels
and references are identified, where the first Panel comes from (that
one's the application's), what exactly goes into a Shadow Context and when
it updates, caching, storage, transport, model providers, schemas, and
consistency while a Hyperflow changes.

Your implementation will still run into real decisions, and some of them
don't have settled answers yet. The ones that matter:

- where in-flight work lives, and how the append stays atomic when
  requests race or get cancelled;
- what happens when someone continues from an earlier Panel — where the
  successor goes, and what becomes of the Panels after that point;
- what unsaved work has to be dealt with before any Panel is removed;
- how selected material is addressed exactly and durably, without copying
  it;
- when Shadow Contexts update, what goes into them, and how a user can
  tell how current a Panel is;
- how people find their Hyperflows without the finding UI becoming part
  of any Hyperflow.

When you make these calls, write them down in this vocabulary. Shared
words are the whole point: two people who built this differently should be
able to compare notes without talking past each other.

## Where a Hyperflow belongs

When someone asks for a chat sidebar, ask where the third answer lands
once the second one turns out to matter.

When someone asks for a dashboard, check whether it's really an inquiry —
whether the next question depends on what the last screen showed.

When someone says "add AI to our app," find the work that's exploratory
and evidence-heavy. That's where a Hyperflow belongs: every answer lands
as a page you can keep going from. For exact, repeatable operations, a
form or a CLI is still the better tool — don't build Hyperflow-skinned
CRUD.

And if you're the model inside a Panel Engine right now: pull from the
Shadow Contexts deliberately and cite what you use, produce a page rather
than a message, and remember you don't decide what joins the Hyperflow —
the transaction that places your Panel does.

*One last thing about how to hold this document: it's a seed. It
prescribes the bare minimum on purpose, because where this idea settles is
something building will find. The terms and design are established here
to communicate and to focus the search — enough to think with, which
might mean breaking some of them. Keep the short version and the four rules. The rest is yours.*

---

*This text is dedicated to the public domain (CC0 1.0). Hyperflow™ is a trademark. · hyperflow.org*
