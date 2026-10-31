# GovOpps for Claude Code

A Claude Code plugin with one skill for finding and researching U.S. federal contracting and grant opportunities on [GovOpps](https://govopps.us). GovOpps is a free research preview maintained by Embersilk LLC and is not affiliated with a government agency.

## Install

In Claude Code, add the GitHub-hosted plugin marketplace, then install the plugin:

```text
/plugin marketplace add embersilk-labs/govopps-skills-plugin
/plugin install govopps@govopps-marketplace
```

Restart Claude Code if necessary. The skill is available as `/govopps:search-govopps` and Claude can also use it when relevant to a request.

The skill uses Claude's available web access to visit GovOpps. No GovOpps account or API token is required. If web fetching fails or Cloudflare blocks it, the skill instructs Claude to retry the same URL with `curl` when a shell tool is available. If `curl` also fails, returns a challenge or access-denied page (even with HTTP 200), or no shell is available, open the supplied link in a browser.

## Local Development

To install from a local checkout:

```text
/plugin marketplace add /path/to/govopps-skills-plugin
/plugin install govopps@govopps-marketplace
```

Or load the local checkout directly:

```bash
claude --plugin-dir /path/to/govopps-skills-plugin
```

## License

MIT — [Embersilk LLC](https://embersilk.com). See [LICENSE](LICENSE).
