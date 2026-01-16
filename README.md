# SearXNG Railway

A pre-configured SearXNG template for Railway, optimized for LLM tool use.

## Features

- JSON and HTML output formats enabled
- GET method for simple query-string API access
- No rate limiting (suitable for private instances)
- Extended timeouts for reliable results (10s/20s)
- Curated search engines with weighted results
- Academic/research engines included (arxiv, semantic scholar, etc.)
- Redis caching support via environment variable

## Deploy

### Railway

[![Deploy on Railway](https://railway.com/button.svg)](https://railway.com/deploy/5vM9JY?referralCode=NhCCIt&utm_medium=integration&utm_source=template&utm_campaign=generic)

1. Deploy this repo
2. Add a Redis service
3. Set environment variables:
   - `SEARXNG_SECRET_KEY` - any random string
   - `SEARXNG_REDIS_URL` - use Railway's Redis connection string

### Any Container Platform

```bash
docker build -t searxng .
docker run -p 8080:8080 \
  -e SEARXNG_SECRET_KEY=your-secret \
  -e SEARXNG_REDIS_URL=redis://your-redis:6379/0 \
  searxng
```

## Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `SEARXNG_SECRET_KEY` | Secret key for the instance | Yes |
| `SEARXNG_REDIS_URL` | Redis connection URL for caching | No |

## API Usage

```bash
# Basic JSON search
curl "https://your-instance/search?q=python+async&format=json"

# Target specific engines
curl "https://your-instance/search?q=transformers&format=json&engines=arxiv,semantic+scholar"

# Paginate results
curl "https://your-instance/search?q=rust&format=json&pageno=2"

# Filter by time
curl "https://your-instance/search?q=news&format=json&time_range=day"
```

## Enabled Search Engines

**General:** DuckDuckGo, Brave, Qwant, Mojeek

**Code:** GitHub, StackOverflow, GitLab, Codeberg

**Docs:** MDN, Arch Wiki

**Packages:** NPM, PyPI, Crates.io, pkg.go.dev, Docker Hub

**Academic:** arXiv, Semantic Scholar, CrossRef, PubMed

**Reference:** Wikipedia, Wikidata, Wikibooks, Currency

**Disabled:** Google, Bing, Yahoo, Yandex, Baidu

## License

MIT
