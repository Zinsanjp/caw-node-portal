# CAW Node Portal (mock)

A single static page that lists CAW nodes and measures, from the visitor's browser, the round-trip time to each one every 5 seconds.

This is an unofficial mock. The page starts from a snapshot of `/api/instances` taken on 2026-10-25 (duplicate registrations removed), then builds the list live: the visitor's browser fetches `/api/instances` from every node on the page and merges the lists. Comments are placeholders.

Live list:

- An entry shows "Listed by M of N nodes": how many of the nodes with a complete list have that registration in their registry data. It is not a vote. An entry that only one node has is just that node's claim.
- A node whose list is empty, or much shorter than the median (less than half), gets a "Some issues" badge and is left out of M and N; otherwise a node that lists only its own registrations would look like the best-agreed entry. The badge is about the list that node returns (for example its registry sync), not a verdict on the whole node.
- Cards are ordered: responding nodes with a complete list first, then the ones with "Some issues", then the ones that did not answer (by name within each group).
- New URLs found in the lists are added (up to 40 cards) and measured too.
- Only plain `https://` hostnames are measured or linked: no other scheme, port, credentials, path, IP address or internal name. Anyone can register any string in the registry, so this keeps the page from being used to open `javascript:` links or to probe the visitor's local network. Entries with other URLs are counted, not shown.

## Use

Open `index.html` in a browser. No build step, no server.

## Caution

The node list comes from the on-chain instance registry, where anyone can register any URL (`registerInstance` is permissionless). A listed node is not verified as legitimate; the page says so next to the list.

## Badges

Each card shows what can be checked from here. None of them proves that a node is legitimate.

- "Registered by its own key": the registry's `owner` (the account that sent the registration transaction) equals its `validatorAddress`, so the registrant controls that key. It does not show who runs the server behind the URL.
- "Active in registry": at least one registration for the URL is active.
- "Listed by M of N nodes" / "Not in the live lists": see the live list above.
- "Responding": measured live, from the visitor's browser.
- "Hand-picked": nodes we chose by hand, shown apart from the registry list.

## Not included

- The CAW logo and the Fraunces font. The upstream repository has no license file, so the logo is not redistributed here. Without them the page falls back to Georgia/serif and shows no logo.
- Latency is measured by the browser, so a node must allow cross-origin requests (CORS) to be measured.
