# Pipeline

*At first, this page will just lay out the roadmap or thinking for completing the assingment.*

In general, the assignment is to engineer an [automated information capture pipeline](./PIPELINE.md) to capture external information for potential inclusion in your book. Since mdBook lacks a direct clipper plugin ecosystem, the workflow will be more deliberate. Create a separate inbox directory outside the mdBook src folder. Configure tools like an RSS reader (e.g., Feedly) with IFTTT/Zapier or custom scripts to automatically save interesting articles, paper abstracts, or email newsletters as raw Markdown files into this inbox. This creates an "editorial funnel." The manual process of reviewing these drafts, refining them, and then consciously moving them into the src directory and adding them to SUMMARY.md becomes a key part of the engineering process, ensuring only curated content makes it into the final publication.

Four approaches are being considered.  I am leaning toward [Approach 4](#approach-4-hybrid-mdbook-centric-system-with-browser-clippers-and-ai-preprocessing), but I would like to capture as much of the advantages as possible from the other three approaches as I adapt [Approach 4](#approach-4-hybrid-mdbook-centric-system-with-browser-clippers-and-ai-preprocessing) going forward.

### Approach 1: Adapt an Existing Open-Source Self-Hosted RSS Reader (e.g., NewsBlur or Alternatives)

[NewsBlur](https://github.com/samuelclay/NewsBlur) can be seen as a potential starting point or stalking horse for a starting point until something better is identified, this approach focuses on self-hosting it or a similar tool, then extending it with custom scripts for Markdown export and GitHub integration. NewsBlur is a Python/Django-based RSS reader that supports feed aggregation, story filtering (e.g., by tags, keywords, authors), and self-hosting via Docker. While it doesn't natively export to Markdown, its open-source nature allows modification. Alternatives like FreshRSS (PHP-based, lightweight, customizable with extensions) or Miniflux (Go-based, minimalistic, supports OPML imports and API for exports) could be easier to adapt if the development of NewsBlur feels too heavy.

#### Steps:
1. **Set Up the Reader**: Clone and deploy NewsBlur using Docker (run `make nb` for containers including databases and web servers). For alternatives, install FreshRSS via Docker or a web server—it's simpler with built-in mobile app support.
2. **Configure Feeds**: Add RSS sources for articles, paper abstracts (e.g., arXiv feeds), and newsletters. Use filters to auto-tag or highlight relevant content.
3. **Extend for Export**: Write a custom Python script (using libraries like feedparser for RSS parsing and markdownify for HTML-to-Markdown conversion) to query the reader's API/database, convert saved/favorited items to raw Markdown files. Schedule this with cron jobs to run periodically.
4. **Push to Inbox**: Use the GitHub API (via PyGitHub library) in the script to commit Markdown files to your PKE repo's `src/1.Projects/inbox` subfolder (create it if needed). This keeps it outside the main src but within Projects for development.
5. **Curation Workflow**: Manually review files in the inbox, refine them (e.g., add metadata like tags or links to SUMMARY.md), and move to appropriate src sections. For automation, integrate an LLM script (e.g., using Hugging Face models) to summarize or classify content before pushing.
6. **AI Integration Path**: Once stable, hook into your MCP vision by treating the inbox as a RAG (Retrieval-Augmented Generation) source for AI agents that curate and suggest additions to the mdBook.

#### Pros:
- Leverages proven RSS functionality (e.g., NewsBlur's social features for potential collaboration).
- Fully open-source and customizable, aligning with your PKE principles of extensibility.
- Alternatives like Miniflux have APIs that make scripting easier than NewsBlur's setup.

#### Cons:
- Self-hosting requires server resources (e.g., VPS for Docker); NewsBlur's setup involves multiple containers, which might be overkill initially.
- Initial extension work needed for Markdown export.

This builds on existing wheels like NewsBlur, as you suggested, and fits your preference for open-source tools similar to Feedly.

### Approach 2: Use No-Code Integrations with IFTTT/Zapier for RSS-to-GitHub Automation
If you want a quicker start without heavy coding, use no-code platforms like IFTTT or Zapier to handle RSS ingestion and file creation in GitHub. These can act as your "editorial funnel" by triggering on new feed items and saving them as Markdown. For a free alternative, use Actionsflow (a GitHub Actions-based Zapier clone) to keep everything in your repo ecosystem.

#### Steps:
1. **Set Up Triggers**: In Zapier/IFTTT, create a "Zap" or "Applet" with RSS as the trigger (e.g., new item in a feed from arXiv or newsletters). Filter by keywords to capture only pertinent content.
2. **Convert to Markdown**: Use built-in formatters or a intermediate step (e.g., Zapier's code block with JavaScript) to extract title, summary, and content, then format as basic Markdown (e.g., `# Title\n\nExcerpt...`).
3. **Push to GitHub**: Connect to GitHub integration to create a new file in your PKE repo (e.g., `src/1.Projects/inbox/new-article.md`). IFTTT has direct RSS-to-GitHub applets for creating issues or commits; Zapier can append to files or create pull requests.
4. **Inbox Management**: Files land in the inbox for manual review. Use GitHub Actions in your repo to auto-label or notify you of new files.
5. **Enhance with Scripts**: For better Markdown quality, add a custom GitHub Action (e.g., from repos like keiranlovett/rss-feed-to-markdown) that runs on push to refine files.
6. **Towards Automation**: Upgrade to AI-assisted curation by integrating Zapier with an LLM API (e.g., OpenAI) to summarize/refine before saving. This aligns with your MCP goal, where the mdBook becomes context for AI-driven filtering.

#### Pros:
- Minimal setup time; no self-hosting needed.
- Handles automation like saving abstracts or newsletters out-of-the-box.
- Free tiers available (e.g., IFTTT for basic RSS triggers); Actionsflow is fully free and GitHub-native.

#### Cons:
- Limited customization (e.g., Zapier might not handle complex Markdown conversion perfectly).
- Dependency on third-party services, which contrasts with your open-source preference—mitigate with Actionsflow.

This is ideal for prototyping your funnel before building custom elements.

### Approach 3: Build a Custom Script-Based Pipeline with Python and GitHub Actions
For full control within your mdBook ecosystem, create a bespoke pipeline using Python scripts and GitHub Actions. This leverages your PKE repo directly, treating the inbox as a staging area in `src/1.Projects`. Tools like feedparser (for RSS) and GitHub Actions ensure it's automated and extensible.

#### Steps:
1. **Script Development**: Write a Python script using feedparser to fetch RSS feeds, markdownify to convert HTML content to Markdown, and frontmatter to add metadata (e.g., source URL, date). Save as individual .md files locally.
2. **Scheduling**: Run the script via cron on a local machine/server or as a GitHub Action workflow (e.g., scheduled daily). Use repos like myquay/feedmd as a base—it's a CLI for converting feeds to Markdown digests.
3. **GitHub Integration**: In the script or Action, use Git commands or the GitHub API to push files to `src/1.Projects/inbox`. Configure the workflow to commit only if new content matches criteria (e.g., via regex filters).
4. **Review Process**: Use mdBook's preview server to view inbox files separately. Manually move refined files to src and update SUMMARY.md.
5. **Automation Evolution**: Add AI layers (e.g., integrate with torch or sympy for content analysis) to auto-curate: classify relevance, generate summaries, or even propose SUMMARY.md updates. This directly supports your vision of the mdBook as a foundation model, where scripts feed into MCP for AI-assisted engineering.
6. **Expansion**: Incorporate email newsletters via IMAP parsing in the script, or web scraping for non-RSS sources.

#### Pros:
- Highly tailored to PKE's structure (e.g., P.A.R.A. organization) and your AI goals.
- No external hosting; runs on GitHub for free.
- Easy to version-control the pipeline itself in the repo.

#### Cons:
- Requires scripting knowledge, though starting with existing repos minimizes this.
- Manual setup for feeds and filters initially.

This approach emphasizes deliberate workflow, as mdBook lacks plugins, and scales to your automated curation objective.

### Approach 4: Hybrid mdBook-Centric System with Browser Clippers and AI Preprocessing
To stay as close as possible to mdBook without external readers, use browser-based clippers combined with scripts for ingestion. This treats your toolchain as an "editorial funnel" extension of mdBook, potentially forking mdBook for custom preprocessors later.

#### Steps:
1. **Clipping Tools**: Use open-source clippers like MarkDownload (browser extension that saves web pages as Markdown) or adapt Obsidian's web clipper. Configure to save clips to a local folder synced with GitHub (e.g., via Git).
2. **RSS Integration**: Pair with a simple RSS poller script (Python with feedparser) that fetches items, uses requests to get full content, converts to Markdown, and saves to the synced inbox.
3. **GitHub Sync**: Use GitHub Desktop or Actions to pull/push the inbox folder in `src/1.Projects`.
4. **Preprocessing**: Develop a Rust-based mdBook preprocessor (as hinted in your curriculum's Phase 4) to scan the inbox, apply AI filters (e.g., via local models), and suggest integrations into SUMMARY.md.
5. **Full Automation**: Evolve to use IFTTT for clipping triggers or Zapier for RSS, but route everything through scripts that enforce curation rules.
6. **MCP Tie-In**: Design the pipeline to output structured data (e.g., YAML frontmatter in MD files) that serves as context for AI models in your MCP infrastructure.

#### Pros:
- Keeps everything within mdBook's ecosystem, per your preference.
- Flexible for non-RSS sources like emails or abstracts.
- Directly advances your AI-assisted knowledge engineering goal.

#### Cons:
- More fragmented initially (clipper + scripts vs. unified reader).
- Requires building/forking mdBook extensions for seamless integration.

These approaches start simple (no-code) and scale to complex (custom AI), aligning with your 100-day PKE curriculum's phases—e.g., foundation in Phase 1, deep learning in Phase 2, and synthesis in Phase 4. Begin with Approach 2 for quick wins, then transition to 3 or 1 for longevity.