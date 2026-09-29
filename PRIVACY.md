# Grammy privacy

Grammy is a Mac app that turns what you type or say into a diagram. This page covers what leaves your Mac and why.

## Your prompts and your API key

- Your Anthropic API key is stored in your Mac's Keychain.
- With your own key, diagrams are made by sending your prompt from your Mac straight to Anthropic, using your key. Those requests don't pass through any Grammy server, and I never see them. Anthropic handles them under your own agreement with Anthropic.

## Free diagrams, before you add a key

Without a key, your first few diagrams are free. They're made through Grammy's server, which adds Grammy's own key and passes your request on to Anthropic:

- Your prompt and the diagram pass through the server on their way to and from Anthropic. The server doesn't log or store them, and I don't see them. Anthropic handles them under Grammy's agreement with Anthropic.
- To count how much of the free allowance each Mac has used, the server keeps a Mac code (a one-way hash of your Mac's hardware ID, never the ID itself), what its free diagrams have cost, how many there were, and when it first and last made one. It doesn't keep your IP address.
- The first part of that code is shown in Settings. If you send it to me to ask for more free diagrams, I can match it to that record, and nothing else.

Once you add your own key, Grammy stops using the server.

## Voice

What you say is transcribed by macOS's built-in speech recognition, on your Mac wherever your Mac supports it. Grammy never records or uploads audio.

## Anonymous usage counts (on by default, off in Settings → Privacy)

To see how Grammy is used and where it falls short, the app sends anonymous events to PostHog (US):

- **When:** the app opens, onboarding finishes, a diagram is made or edited, a diagram fails, a diagram is opened in the editor, closed by hand, or given a 👎, and on the free trial: when you start it, when you ask for more, and when you add your own key.
- **What's in them:**
  - a random install ID and a random ID per diagram
  - the app and macOS versions
  - typed or spoken, and the model used
  - whether you're using your own key or the free trial
  - timings
  - the prompt's length in words
  - the diagram's type (for example "funnel" or "quadrant") and how many elements it has
  - how many layout problems the renderer found
  - for failures, what went wrong
- On the free trial, Grammy's server also reports, under the same random install ID, what each free diagram cost and whether a request was turned away. It only does this while usage counts are on.
- **Never in them:** your prompts, your diagrams, your key, or your IP address. There are no personal profiles.

## Sharing a diagram after a 👎

When a diagram isn't right, you can give it a 👎. Grammy then asks **Share with developer?** Only if you tap **Share** does it send, for that one diagram:

- the prompt
- the diagram's description, the text the diagram is drawn from
- the model used
- the same anonymous details as above

That's what lets me reproduce the problem and add it to the tests Grammy is checked against. Shared diagrams are only used to improve Grammy. They're never sold or used for anything else, and they're kept for no more than a year. Sharing works even with the usage counts switched off, because you chose to send it.

Grammy doesn't know who you are. To have a diagram you shared removed, [open an issue](https://github.com/amanmathur99/grammy-releases/issues) saying roughly when you shared it and what it was about, and it will be deleted.

## On your Mac only

- Your diagram history.
- The logs in `~/Library/Logs/Grammy/`. They record failures and, for recordings, timings and word counts, never the words.
