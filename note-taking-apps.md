# 5 Note-Taking Apps You Should Try Before Forgetting All of Them and Using the Command Line.

Keeping my thoughts, todos, and notes organized has been essential to managing my workflow and generally keeping on top of things.  Over the years I've sampled a variety of tools in search of that silver bullet that will finally make everything come into place.  

This is everything I was looking for in a perfect note-taking implement:

- Portable
- Permanent
- Minimalistic
- Fast
- Searchable
- Secure
- Hackable
- Free

While experience tells me that no such tool exists, I wanted to find my local optimum.  This is the story about how I got there by eschewing the fancy apps and embracing simplicity.

## "Good Old" Pen & Paper

Does this mean that I've come around to scribbling like a cloistered monk in the Dark Ages? Not quite. 

Don't get me wrong, I love the feeling of a Zebra F-301 smoothly gliding over a moleskin sheet.  But I've found handwriting to have its share of problems, possibly due to my poor life skills. Here's an artist's depiction of what I might find on my desk in the midst of a Luddism kick:

![Pic of Simulated Paper Todo List](img/paper-todo-list.jpg)

Blasticate the who now?  And what is that, ketchup[^eating]?  Maybe I need to improve my handwriting skills, or maybe my hand and brain are just never going to get along.  Even if I could write beautifully and legibly, exercising my penmanship doesn't work so well in practice due to a few critical pain points:

1. I'm always forgetting to bring my notebook around.
2. Due to excessive short-hand, I can't comprehend what I wrote 2 weeks ago.
3. Writing does not work at the speed of my brain.
4. Searching for something in particular?  That's quite an I/O-bound process.

I really tried to make this old-school medium work for me, but I just couldn't stick to it.  Maybe if there was something more...sticky.

## Desktop Stickies

I'm not spoiling for a fight about [Skeuomorphism], but I did give desktop stickies a try for about a week after I saw how my manager was using it.  I liked a few things about it: writing a note was really quick, as I could do it with a few keystrokes and get back into my workflow without breaking a sweat.  Whenever I needed to find a note, it was right there on my Desktop waiting for me.

There is one big drawback though. Frequent application of Stickies leads to this symptom:

![Desktop full of Sticky Notes](img/desktop-full-of-sticky-notes.jpg)

They quickly devolve into clutter, and there's no easy way to manage it. Minimizing them is a pain, and you want to save them you have to store each one to a separate file, choose the directory, and so on.

Also, you can't easily search stickies, or access them on a mobile device.  The improvement over physical paper is only slight, and the I've found that the drawbacks are even worse.  It fails my need for permanence, minimalism, portability, and searchability.  

That said, it's sometimes useful to stick a note on your Desktop as a reminder, so there's still a use case for this app.  Recently, though, I've found something better for this purpose.

## Hoverpad

One of my co-workers recently released a nice little utility in the App Store called [Hoverpad] and I decided to give it a spin.  It's a bit like Stickies in that it places a permanent window on the Desktop, although it's layered above all the other windows and easily hidable.  The tool is refreshingly minimalistic, has excellent hotkey support, and offers a convenient paste-bin feature. 

![Hoverpad Screenshot](img/hoverpad-screenshot.jpg)

Since it shares a lot of the same attributes as Stickies, Hoverpad didn't meet most of my requirements for note-taking, but it filled a need in my day-to-day workflow to keep my priorities visible and help shuttle paste buffer contents around.  

In a relentless search to achieve my primary goal, I had to move onto something designed for long-form notes.

## Mac Notes

I really like Notes for the same reasons I like [Preview].  Notes only does a few things, and does them really well.  When you connect to an account (Gmail, Exchange, etc) the notes sync quickly and seamlessly across Mac and iOS.  I find this to be a great way of transferring text back and forth between my phone and my laptop, and still use it frequently for this purpose.

![Mac Notes Screenshot](img/mac-notes-screenshot.jpg)

There's one thing about Notes that stuck in my craw though:  I didn't want to keep my life's thoughts locked into the Apple ecosystem.  If I ever migrated from iOS to Android, I'd be totally screwed.  The portability/hackability/free requirement was not met.

Also, I missed built-in encryption support provided by Evernote, which is essential to keeping secrets like password hints.  For cross platform copy-and-paste, it's pretty slick though.

## Back to Evernote

[Evernote] is a well-featured, robust product that I proselytized for many years.  It's a common platform for recording every possible thing you want to remember, and it supports some nice features like encryption, multimedia, and a smorgasbord of [cross-app integrations]. 

At some point, I fell off the wagon, and decided to give it another try.  That's when I realized why I quit using it in the first place.

![Evernote Screenshot](img/evernote-screenshot.jpg)

Wow, there's a lot going on in the UI.  Where do I even click to start a new note?  Clicking is for chumps anyway, cmd-N work well enough.

As I entered my notes I found myself distracted by the large amount of clutter in the interface that had no bearing on my primary intent.  It was like driving in a nail with a nuclear bomb, or however that analogy is supposed to go.

Evernote suffers a host of other pain points:

- It has become an increasingly bloated client over time, though the [web app] is better in this respect.
- Like Mac Notes, you need a closed-source binary app to access your notes.
- Frequent chicanery like encouraging photo uploads so you hit your free disk space limit.
- Occasional in-app advertising, which is expected for a free service, though annoying.
- Not a free or open-source solution

I think this application can work wonders for a lot of use cases, and I would definitely encourage others to [try Evernote] if they haven't already. However, I was disturbed by the nag-factor of the premium up-sells and the obvious lack of control over my own data.   The portability of Evernote is pretty good, but it utterly fails my requirements for minimalism, hackability, and freedom.

Surely there must be a better way?

## Enter the CLI

A recent Google search led me to a [lifehacker article] detailing a simple note-taking tool that was usable from the command line.  If fact, the implementation was so trivial that it fit in the content of the article.  Here it is, modified a bit with the suggestions pulled from some of the article comments:

```sh
n() {
  mkdir -p "${NOTE_DIR:-~/notes}"
  ${EDITOR:-vim} "${NOTE_DIR:-~/notes/}""$1".txt
}
nls() {
  ls -c "${NOTE_DIR:-~/notes}" | grep "${1:-.}"
}

# Edit/start a note:
# $ n my-note

# List notes
# $ nls [query]
```

The mechanism is trivial and based on file/folder semantics.  You have a folder called "notes" in your home directory.  This folder is a flat namespace containing text files.  The filename is the label for the note.  That's it.

I've been trying this out for about a month, and I'm really digging it.  I don't have to leave the command line to take a note, and I love the fact that I'm retaining full control of my data.  It was easy to add [many more features] to the script, such as search and basic encryption support, and I found that by symlinking my notes directory into [Dropbox], I got instant cloud backups and mobile read-only access.

Of course, there are a few minor shortcomings.  It's not highly portable (no editing on mobile), and I have to depend on Dropbox for permanence, which is a compromise to avoid monthly cloud storage costs.  No solution is perfect, but this happens to be the best that I've found.

## Final Note

My quest to find the perfect note-taking tool has taught me one thing: I hate taking notes. The simpler the solution, the more likely I am to do it.  For those comfortable with the command line, it might be worth giving the [CLI technique] a spin, and for others, Evernote, Mac Notes, or Notepad.exe might be the perfect solution.

Lesson: Do whatever works for you and helps you remember stuff.

_Chris Carpita is a Software Engineer at Spotify and likes doing big things while typing little._

[^eating] Fact: _Real_ software engineers eat at their desks.  Whoever wrote _[Never Eat Alone](http://www.amazon.com/Never-Eat-Alone-Secrets-Relationship/dp/0385512058)_ never debugged anything four hours before release.

[lifehacker article]: http://lifehacker.com/5592047/turn-your-command-line-into-a-fast-and-simple-note-taking-tool
[CLI technique]: http://github.com/ccarpita/nota-bene
[many more features]: http://github.com/ccarpita/nota-bene
[cross-app integrations]: https://appcenter.evernote.com/
[web app]: http://blog.evernote.com/blog/2014/10/02/new-beautiful-evernote-web/
[Hoverpad]: https://itunes.apple.com/us/app/hoverpad-notepad-+-clipboard/id931401484?mt=12
[Skeuomorphism]: http://www.themachinestarts.com/read/2012-11-how-we-started-calling-visual-metaphors-skeuomorphs-why-apple-design-debate-mess
[Preview]: http://www.macworld.com/article/2010521/the-hidden-powers-of-mountain-lions-preview.html
[Dropbox]: http://www.dropbox.com
