# draw.io Embed Lab

A dependency-free demo of the official diagrams.net embed mode and GitHub Markdown workflow.

![Architecture diagram](diagrams/architecture.drawio.svg)


## GitHub Markdown

GitHub renders an editable PNG or SVG like any other image:

```markdown
![Architecture diagram](diagrams/architecture.drawio.svg)
```

The checked-in SVG includes a copy of the diagram XML in its `content` attribute. For diagrams exported manually, select **File > Export as > SVG** and enable **Include a copy of my diagram**.

To edit files directly in a GitHub repository, use the built-in GitHub storage mode:

- [Open diagrams.net in GitHub mode](https://app.diagrams.net/?mode=github)
- Template URL format: `https://app.diagrams.net/#U<URL_ENCODED_RAW_GITHUB_URL>`
- Direct GitHub URL format: `https://app.diagrams.net/#H<OWNER>%2F<REPOSITORY>%2F<BRANCH>%2F<PATH>`

For example, after publishing this repository, a direct edit link has this shape:

```text
https://app.diagrams.net/#HOWNER%2FREPOSITORY%2Fmain%2Fdiagrams%2Farchitecture.drawio.svg
```

## How embedding works

The host loads `https://embed.diagrams.net/?embed=1&proto=json` in an iframe and uses the HTML5 Messaging API:

1. diagrams.net sends `{ "event": "init" }`.
2. The host sends `{ "action": "load", "xml": "..." }`.
3. diagrams.net sends `{ "event": "save", "xml": "..." }`.
4. The host requests an `xmlsvg` export and updates the preview.

Messages are accepted only from `https://embed.diagrams.net` and the known iframe window.

## References

- [Embed a diagram in GitHub Markdown](https://www.drawio.com/docs/integrations/github/diagrams-in-github-markdown/)
- [Embed mode reference](https://www.drawio.com/docs/reference/embed-mode/)
- [jgraph/drawio-github](https://github.com/jgraph/drawio-github)
- [jgraph/drawio-integration](https://github.com/jgraph/drawio-integration)