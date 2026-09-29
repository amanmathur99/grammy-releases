# Grammy privacy

Grammy is a Mac app that turns what you type or say into a diagram. This page covers what leaves your Mac and why.

## Your prompts and your API key

- Your Anthropic API key is stored in your Mac's Keychain.
- Diagrams are made by sending your prompt from your Mac straight to Anthropic, using your key. Those requests don't pass through any Grammy server, and I never see them. Anthropic handles them under your own agreement with Anthropic.

## Voice

What you say is transcribed by macOS's built-in speech recognition, on your Mac wherever your Mac supports it. Grammy never records or uploads audio.

## Anonymous usage counts (on by default, off in Settings → Privacy)

To see how Grammy is used and where it falls short, the app sends anonymous events to PostHog (US):

- **When:** the app opens, onboarding finishes, a diagram is made or edited, a diagram fails, a diagram is opened in the editor, closed by hand, or given a 👎.
- **What's in them:**
  - a random install ID and a random ID per diagram
  - the app and macOS versions
  - typed or spoken, and the model used
  - timings
  - the prompt's length in words
  - the diagram's type (for example "funnel" or "quadrant") and how many elements it has
  - how many layout problems the renderer found
  - for failures, what went wrong
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
