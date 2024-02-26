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

* abstract type - XXX

* array - a Janet data structure that is a mutable array.
  XXX: describe literal form?

* binding - association between a value and a symbol - XXX: lexical
  immutable created by `def`, lexical mutable created via `var`, and
  dynamic mutable changed via `setdyn` (accessed via `dyn`)

* boolean - a Janet data structure with two values, true and false.

* buffer - a Janet data structure consisting of a mutable sequence of
  bytes.  There are two literal forms.  One form starts with the @
  character, followed by a double quote character, roughly the buffer
  content, and then finally by another double quote character.  For
  the other form, see "long-buffer".

* bytes type - a Janet string, buffer, symbol, or keyword

* c function - XXX

* channel - one of two methods of communication between tasks.  (See
  stream for another.)

  * ordinary, non-threaded - allows the programmer to communicate by
    sending any Janet value as messages, and only work inside a thread
    \- they do not allow communication between threads, processes, or
    over the network.

  * threaded - allows the programmer to communicate Janet values
    between threads.  XXX: limits of the sorts of things that can be
    transferred is not so clear.

* dictionary type - a Janet struct or table

* environment - XXX

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

* function - XXX

* indexed type - a Janet array or tuple

* keyword - a Janet data structure consisting of an immutable sequence
  of bytes.  The literal form starts with a colon character.

* loader - XXX

* long-buffer - a Janet syntactic literal that when parsed, results in
  a Janet buffer.  A long-buffer starts with the @ character, followed
  by some number of backticks, roughly the buffer content, and then
  ending with the same number of backticks as those that came
  immediately after the @ character.

* long-string - a Janet syntactic literal that when parsed, results in
  a Janet string.  A long-string starts and ends with the same number
  of backtick characters.

* macro - XXX

* metadata - XXX

* module - a collection of bindings and associated environment

* nil - a Janet data structure that represents "no value".

* number - a Janet data structure representing a number.  The
  underlying represention uses IEEE 754 floating point numbers.
  XXX: there are multiple literal forms.

* peg - parsing expression grammar.  XXX

* peg special - XXX

* prototype table - XXX

* scope - a specific scope is where certain bindings are valid

* signal - a value "raised" by a fiber during its execution.  an
  ancestor fiber that has an appropriate "mask" can trap / block /
  capture (and examine) such values and take some kind of action.

  note that this kind of signal is different from a POSIXy system's
  signal.  For that type of signal, see `os/proc-kill` and
  `os/sigaction`.

* special form - XXX

* stream - one of two methods of communication between tasks.  (See
  channel for anotrher.)  They are wrappers around file descriptors
  and operate on streams of bytes.  Streams can communicate across
  threads, processes, and across the network.

* string - a Janet data structure consisting of an immutable sequence
  of bytes.  There are two literal forms.  One form is bounded at the
  start and end by double quotes.  For the other form, see
  "long-string".  XXX: mention escaping?

* struct - a Janet data structure that is an immutable associative
  array.  The literal form is bounded at the start with an opening
  curly brace and at the end by a closing curly brace.  Between the
  braces there can be an even number of Janet expressions.

* symbol - a Janet data structure consisting of an immutable sequence
  of bytes, typically used for naming other values.  The literal form
  is the sequence of bytes.  XXX: mention legal byte sequences?

* table - a Janet data structure that is a mutable associative array.
  XXX: describe literal form?

* thread - XXX

* tuple - a Janet data structure that is an immutable array.  XXX:
  describe literal forms (square bracket and paren) and typical use?

## Notes

May not be helpful to be too dry.  Providing specific examples and
code before definitions may be much more helpful.

## Credits

* amano.kenji - code, discussion, feedback
* bakpakin - code, discussion, janet
* llmII - code, discussion, feedback
