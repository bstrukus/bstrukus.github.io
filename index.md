---
layout: default
---

{% assign headshot = site.static_files | where: "path", "/assets/images/headshot.jpg" | first %}
{% if headshot %}
<img src="{{ '/assets/images/headshot.jpg' | relative_url }}" alt="Headshot of Ben Strukus" width="280">
{% endif %}

Seattle-based improviser, actor, and disembodied voice. Comedic and dramatic, on stage and behind the mic. After 15 years building games, I'm bringing that plus 130+ improv shows to voice work for games and animation.

**Voice credit:** *Sail Forth* · **Training:** Drew Hobson

[Demos](#demos) · [About](#about) · [Credits](#credits) · [Contact](#contact)

## Demos

*Coming soon.*

<!--
When a demo is ready, drop the MP3 in assets/audio/ and add a block like this:

### Character
<audio controls preload="none" src="{{ '/assets/audio/character-demo.mp3' | relative_url }}"></audio>
[Download]({{ '/assets/audio/character-demo.mp3' | relative_url }})
-->

## About

Hey! I'm a Seattle-based improviser, actor, and disembodied voice. Comedic and dramatic, on stage and behind the mic.

I grew up on cartoons and video games: heroes, villains, characters who changed because of what they went through. Then I spent 15 years building games and immersive software, which taught me how interactive stories actually get made and how much they can mean to the people playing them. I have a voice credit in *Sail Forth* and train in voice over with Drew Hobson (Xbox, Nintendo, ArenaNet).

I came to performing late, through an improv class in 2023, and fell hard for it. Three years and roughly 130 stage appearances later, I perform regularly at Duos Open Mic at Unexpected Productions, with an indie team, and on the Cabaret Roulette mainstage show at Seattle Comedy Theater. Improv taught me to build a character in real time with other people; now I want to bring that to scripted work. To me, voice acting isn't doing funny voices. It's embodying someone fully enough that a player recognizes a piece of themselves in them. That's the work I want, with people who care about it as much as I do.

## Studio

*Specs coming soon.*

## Credits

**Voice**
- *Sail Forth*

**Stage**
- Cabaret Roulette (mainstage), Seattle Comedy Theater
- Duos Open Mic, Unexpected Productions

**Training**
- Voice over with Drew Hobson

## Contact

{% if site.formspree_id %}
<form class="contact-form" action="https://formspree.io/f/{{ site.formspree_id }}" method="POST">
  <p><label>Name<br><input type="text" name="name" required></label></p>
  <p><label>Email<br><input type="email" name="email" required></label></p>
  <p><label>Message<br><textarea name="message" rows="5" required></textarea></label></p>
  <p><button type="submit">Send</button></p>
</form>
{% endif %}
{% if site.contact_email %}
Email: [{{ site.contact_email }}](mailto:{{ site.contact_email }})
{% endif %}
{% unless site.formspree_id or site.contact_email %}
*Contact form coming soon.*
{% endunless %}
