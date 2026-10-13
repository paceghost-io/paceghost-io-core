# paceghost-io-core

Public data from [Paceghost](https://www.paceghost.io). Paceghost measures how websites appear in search engines and AI answers.

## Contents

| File | What it is |
|---|---|
| `user-agents/known-ai-bots.json` | A list of crawlers, fetchers and robots.txt tokens from AI and search companies. |
| `user-agents/known-ai-bots.schema.json` | The JSON Schema (draft 2020-12) for the list. |

## The crawler list

Each entry gives the name, the robots.txt token, the operator, the purpose, the user agent strings and the robots.txt behavior. Each entry cites a page of the operator and quotes the sentence that supports its purpose. The `readOn` field gives the date we read that page.

If an operator publishes no page about a crawler, the entry has `"source": "none"` and no purpose. We do not take the purpose from third-party lists.

### Classes

| Class | Meaning |
|---|---|
| `training` | The operator says the crawler collects content that can be used to train AI models. |
| `search_index` | Builds an index for a search or answer product. |
| `user_fetch` | Fetches a page when a user asks for it. |
| `agent` | An AI agent that browses and acts for a user. |
| `governance_token` | A robots.txt name that sets how content is used. It is not a separate crawler, for example `Google-Extended`. |
| `ads` | Checks pages for an ad product. |
| `seo` | Collects data for SEO tools. |
| `dataset` | Builds a web dataset that others use. |
| `other` | A documented purpose that fits none of the above. |

### robots.txt behavior

`respectsRobotsTxt` repeats what the operator states: `yes`, `no`, `partly`, `not_stated`, or `not_applicable`. The `robotsTxtQuote` field gives the sentence. We did not test the behavior.

Some crawlers have no robots.txt token. Some agents identify themselves with a Web Bot Auth signature instead. The `webBotAuth` field gives the signature agent and the key directory.

### Example

```json
{
  "name": "OAI-SearchBot",
  "token": "OAI-SearchBot",
  "operator": "OpenAI",
  "class": "search_index",
  "respectsRobotsTxt": "yes",
  "source": "https://developers.openai.com/api/docs/bots",
  "quote": "OAI-SearchBot is used to surface websites in search results in ChatGPT's search features.",
  "readOn": "2026-10-13"
}
```

The example leaves out some fields. See the JSON file for the full entry.

## PaceghostBot

Paceghost's own crawler is in the list. Its page is [paceghost.io/resources/paceghostbot](https://www.paceghost.io/resources/paceghostbot/).

Paceghost also runs a second bot, `PaceghostResearchBot`. It reads public websites of German companies to find a postal address for one postcard about Paceghost. It follows robots.txt. It is not an AI or search crawler, so it is not in the JSON. Its notice, in German, is at [paceghost.io/researchbot.txt](https://www.paceghost.io/researchbot.txt).

## Corrections

If an entry is wrong or a crawler is missing, open an issue with a link to the operator's own page.
