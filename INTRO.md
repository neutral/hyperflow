# Hyperflow

*The walk-through. The model itself is [SPEC.md](SPEC.md) — after this
page it should feel obvious.*

## The drawer

So you've been asked to add AI to your app, and you already know what
you're going to build: chat panel on the right, textbox at the bottom,
answers piling up in a transcript. Everybody's shipping one.

It kind of works, the first time. Someone asks about a spike in the error
table and an answer appears in the drawer. The trouble starts with the
second question — the first answer has scrolled away from the rows it was
explaining, and it never could touch those rows anyway.

Keep one question in mind for the rest of this page: when an answer comes
back, where does it land, and what does the next one know?

## Let the answer be a page

Hyperflow's first move is the whole idea in miniature: the answer isn't a
message, it's a Panel — like a web page with one job, opening next to the
page it came from. Ask about the spike and you get a page about the spike. And
because it's a page, it does what pages do: you can select from it,
refresh it, keep it, and act on it, with the same muscle memory as the
rest of your app.

## One trail, in order

Panels line up in the order you asked for them. That ordered trail is a
Hyperflow. Compare it to what you'd otherwise have by Friday: nineteen
tabs you have to re-explain to yourself, or a canvas you arrange by hand.
In a trail, scroll back and every earlier panel still works, and the
order itself tells the story of the investigation. It's meant to be kept,
too — pin it, come back Monday, hand it to a teammate.

## Ask by marking

Both ways of getting the next panel are marking. A page can ship with
Highlights — phrases marked ahead of time, each with a prompt behind it,
at the places readers keep needing to go deeper. Click one and the next
panel opens. And when nobody predicted your question — say, two rows that
look wrong together — you mark it yourself: select the rows, attach a
sentence, ask. That's an Annotation.

Notice what's not on that list: links. A link can only take you to a page
somebody already built, so Hyperflow leaves links exactly as they are.
Clicking a hyperlink inside a panel is just the web; the trail doesn't
move. Marking grows the trail, clicking never does.

## The trail remembers

Here's what makes the generated panels good instead of generic. Behind
every panel, the engine keeps a shadow context — notes on what that panel
is and what it's currently showing. When a new panel is being generated,
the agent can see all of them, takes what it needs, and the new panel
cites what it took.

Without this you get the two familiar failure modes: the model knows
nothing and answers generically, or the whole transcript gets pasted in
and the answer is grounded in everything while citing nothing. It's also
why a highlight prompt written months ago still lands — it doesn't have
to predict your investigation, because the trail's memory arrives on its
own.

## Refresh still means refresh

A generated panel isn't a screenshot of the moment it was made. Its
layout is fixed at generation, but the data inside is stored as
references and looked up at render time. So refresh means what it has
always meant: same page, current numbers. Open the spike chart a week
later and it shows this week's data — and the shadow context behind it
stays current the same way.

## Four rules keep it a record

Everything above hangs on four short rules: one ordered trail; a request
adds exactly one panel or nothing at all; the trail never gets pasted
into a prompt — that's what shadow contexts are for; and backend actions
never move the trail. They exist so the trail stays something you can
trust as a record of the inquiry. The rest — schemas, caching, storage,
how any of it looks — is explicitly your call. All four are a five-minute
read in [SPEC.md](SPEC.md).

## The name

The web has changed how you get to the next thing twice: hypertext let a
page offer where to go, and chat let you ask for an answer. Hyperflow
keeps a half from each —

hyper~~text~~ / ~~chat~~flow — **Hyperflow**.

Keep hypertext's follow-from-here, drop the rule that every destination
is built in advance. Keep chat's ask-for-anything, drop the transcript as
the shape of the answer. What's left is a trail whose next page can be
followed or formed.

## Where to start

The spec's short version is one paragraph, and the smallest real
implementation is a list of panels and one function. Some parts are still
open questions, and the spec marks them as open instead of pretending.
If you're an agent reading this next to a build request, you already know
the question to ask: where does the answer land, and what does the next
one know?

---

*This text is dedicated to the public domain (CC0 1.0). Hyperflow™ is a trademark. · hyperflow.org*
