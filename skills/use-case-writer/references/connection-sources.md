# Model identifiers and app endpoints

Read the current app configuration, canonical Router guide, and applicable reusable regions before drafting. Connection details depend on the target version and caller. Do not infer the connection from the model's name alone.

| Connection | Identifier source | Endpoint source |
| --- | --- | --- |
| Through Router | The route alias the app accepts, or the complete identifier in Router's How to call this model window | Router's connection example for the caller and API format, unless the app supplies its own default |
| Direct single-model service | The model service's displayed model ID, commonly on its Launchpad page | The model app's relevant entrance in Settings |
| Direct Ollama service | A model actually available in that Ollama instance, such as one listed by `ollama list` | That instance's Ollama API entrance in Settings |
| App API, such as a memory service | The app-specific resource ID, when required | The API entrance for the feature, not its web console or Router URL |

## Router

- Check whether the app uses a default route, an explicit model, or an automatically supplied connection. Do not add manual URL/key setup when working defaults already provide it.
- For an explicit model, preserve the full Router identifier, including its provider prefix. Do not substitute the model app's local display name.
- Treat chat, embedding, and reranking separately. Do not assume that changing a Router default overrides a model explicitly selected by an app. Keep collection/index compatibility requirements visible when changing embeddings.
- Read connection examples for the relevant caller location and API protocol. Base paths and authentication can differ. Do not hardcode a universal `/v1` or API-key rule.
- Look for applicable regions in `docs/reusables/ai-service-connections.md` and their localized counterparts. Verify them before inclusion.

## Direct model services

Use this branch only when the app actually connects to the model service directly. Explain how to get the model ID from that service and its endpoint from Settings. Select the specific API entrance if more than one is available. Do not introduce an additional Ollama installation merely to reproduce an old example.

## App APIs and exact values

Copy the endpoint from the relevant app's Settings or documented connection view. Read the actual Entrances or Shared entrances UI rather than inventing a URL format. Distinguish the agent-to-app API connection from the app-to-model connection.

Read screenshot-only values from the screenshot or confirm them against configuration. If a required identifier, field, or URL remains unknown, mark it explicitly as unresolved in the draft and review summary. A hidden FIXME does not make a guessed value ready to publish.

For SSH, game ports, SFTP, and external clients, also read [Network access](network-access-patterns.md). Web entrance conventions do not apply to every protocol.
