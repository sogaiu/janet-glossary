# janet-glossary

This document is an in-progress attempt to provide a useful glossary
for the Janet programming language.

With a sufficiently coherent and comprehensive glossary, it becomes
more practical to be clearer about which terms are significant, which
terms might be synonyms, and what some of the associated meanings are.

## Motivation

A glossary can provide a consolidated home for names, synonyms, and
definitions of important concepts.  This can be helpful at times for
at least the following:

* improving clarity of communication and thought
* the creation and interpretation of documentation

There seems to be a tendency in typical English writing to push toward
not reusing certain words in nearby text.  Sometimes a specific term
may be avoided and a different one used in its place.  Especially when
dealing with technical concepts, this can be problematic because
particular words have very specific meanings that are not typically
implied when other words are used instead.  It may also happen that
one reaches for pronouns as a coping strategy, but this may also lead
to issues because increased pronoun use can make text harder to
interpret since the amount of guessing tends to increase.  In
addition, sometimes a substituted word may also have a separate
particular meaning from that of the original word and this can lead to
additional confusion.

One hope is that with an appropriate glossary, people can more
practically mitigate some of the downsides of the aforementioned
linguistic peculiarity of English (^^;

## Terms

* channel - one of two methods of communication between tasks.  (See
  stream for another.)

  * ordinary, non-threaded - allows the programmer to communicate by
    sending any Janet value as messages, and only work inside a thread
    \- they do not allow communication between threads, processes, or
    over the network.

  * threaded - allows the programmer to communicate Janet values
    between threads.  XXX: limits of the sorts of things that can be
    transferred is not so clear.

* event loop - provides concurrency within a single thread by allowing
  cooperating fibers to yield instead of blocking forward progress.

* fiber - allows a process to stop and resume execution later,
  essentially enabling multiple returns from a function.

  * ordinary, non-root - the programmer can resume this type of fiber
    using `resume`.  XXX: it's unclear whether there is a
    well-accepted / firmly established term for this.

  * task, root - a fiber that will be automatically resumed when an
    event (or sequence of events) that it is waiting for occurs.  The
    programmer should not try to resume this type of fiber.

    Note that in a standard janet build, a task is the same as a root
    fiber.  The root fiber for the current fiber is the oldest
    ancestor that does not have a parent.  It is obtainable via the
    `root/fiber` function.  A task is sometimes referred to as "a
    fiber that was scheduled to run by the event loop" or "a fiber on
    the event loop".

* signal - a value "raised" by a fiber during its execution.  an
  ancestor fiber that has an appropriate "mask" can trap / block /
  capture (and examine) such values and take some kind of action.

  note that this kind of signal is different from a POSIXy system's
  signal.  For that type of signal, see `os/proc-kill` and
  `os/sigaction`.

* stream - one of two methods of communication between tasks.  (See
  channel for anotrher.)  They are wrappers around file descriptors
  and operate on streams of bytes.  Streams can communicate across
  threads, processes, and across the network.

## Credits

* amano.kenji - code, discussion, feedback
* bakpakin - code, discussion, janet
* llmII - code, discussion, feedback
