# EPLAN documentation RAGs on Cloudflare

Source code for three public documentation search services deployed on Cloudflare Workers. They complement the local EPLAN action server in [eplan-mcp](https://github.com/Canary-ECAD/eplan-mcp) and the guidance in [eplan-scripting-skill](https://github.com/Canary-ECAD/eplan-scripting-skill).

| Project | Documentation | Search | MCP endpoint |
|---|---|---|---|
| [cloudflare-rag-eplan-p8](cloudflare-rag-eplan-p8/README.md) | EPLAN Electric P8 2026 | Vectorize + Workers AI semantic search | https://rag2026.covaga.xyz/mcp |
| [cloudflare-rag-eplan-2027](cloudflare-rag-eplan-2027/README.md) | EPLAN Electric P8 2027 | D1/FTS5 keyword search | https://rag2027.covaga.xyz/mcp |
| [cloudflare-rag-eecpro](cloudflare-rag-eecpro/README.md) | EPLAN EEC Pro 2026 | Vectorize + Workers AI semantic search | https://rageecpro.covaga.xyz/mcp |

The services are already deployed. To use them as MCP servers, configure their HTTPS endpoints in your client; no local index is needed. Each project README documents its tools, REST API, data source and maintenance steps.

## Repository layout

```text
eplan-cloudflare-rags/
├── cloudflare-rag-eplan-p8/      # P8 2026 semantic index
├── cloudflare-rag-eplan-2027/    # P8 2027 API wiki, D1/FTS5
├── cloudflare-rag-eecpro/        # EEC Pro 2026 semantic index
└── .github/workflows/            # Manual P8 Worker deployment
```

## Deployment

The [P8 deployment workflow](.github/workflows/deploy-cloudflare.yml) can be started manually after adding `CLOUDFLARE_API_TOKEN` and `CLOUDFLARE_ACCOUNT_ID` as repository secrets. Moving the source repository does not move GitHub secrets or Cloudflare resources. The EEC Pro and P8 2027 projects have their own deployment instructions in their READMEs.

ChromaDB source data, Vectorize indexes and the D1 database are not stored in this Git repository. The export scripts accept an explicit source path through `EPLAN_P8_CHROMA_DB_PATH` or `EEC_PRO_CHROMA_DB_PATH`; their defaults assume sibling checkouts of the source projects.

## Related repositories

- [eplan-mcp](https://github.com/Canary-ECAD/eplan-mcp): local MCP server that controls a running EPLAN instance.
- [eplan-scripting-skill](https://github.com/Canary-ECAD/eplan-scripting-skill): agent skills and an MCP configuration for these documentation services.
- [Bochica](https://github.com/Canary-ECAD/bochica): Windows desktop app that uses these documentation services out of the box, with eplan-mcp and the skills, behind a chat.

## License

MIT — see [LICENSE](LICENSE).

> **Disclaimer:** this is an independent community project by [Canary E-cad](https://github.com/Canary-ECAD). It is not affiliated with, endorsed by, or supported by EPLAN GmbH & Co. KG. EPLAN, EPLAN Electric P8 and EPLAN EEC Pro are trademarks of their respective owner. The MIT license covers this repository's code only; the documentation these services index belongs to its owner.
