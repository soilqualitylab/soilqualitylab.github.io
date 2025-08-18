# Research Dashboard

*At first, this page will just lay out the roadmap or thinking for completing the assingment.*

In general, the assignment was to create the [Research Dashboard](RESEARCH_DASHBOARD.md) chapter in your mdBook. Since there's no dynamic plugin like Dataview, write a simple Python or shell script that scans your inbox directory for new files or files with a \#summarize tag in their frontmatter, and generates a summary list. This script can be run manually to update the dashboard page. 

[Grok was asked to give suggestions on how to complete this task of building a research dashboard.](https://grok.com/share/c2hhcmQtMg%3D%3D_a61a9454-813a-482d-bb1c-1e1e257dbc39)

### Existing Developments
While there isn't a direct equivalent to Obsidian's Dataview plugin specifically for mdBook (which would allow querying Markdown files like a database and generating dynamic views such as tables or lists), some related tools and plugins are in development or available that could serve as starting points or inspirations for your Personal Knowledge Engineering (PKE) system. Based on recent searches:

- [**mdbook-template**](https://crates.io/crates/mdbook-template): This is a prototypical method for building preprocessor plugin that enables dynamic text generation by allowing you to include Markdown files with customizable arguments (e.g., passing variables to templates for conditional or parameterized content). A simple [mdbook-preprocessor](https://github.com/topics/mdbook-preprocessor) or [mdbook-plugins](https://github.com/topics/mdbook-plugins) for rendering content in interactive tabs, which adds a layer of dynamic presentation to static Markdown. This isn't query-based but demonstrates how plugins can manipulate content structure during build. This does not immediately yield a full query engine like Dataview, but it supports basic dynamic inclusion and could be extended for metadata-based generation. [**mdbook-template**](https://crates.io/crates/mdbook-template) was actively maintained [as a crate on **crates.io**](https://crates.io/) and available on GitHub as the[**mdbook-template** archive repo](https://github.com/sgoudham/mdbook-template). One feasible approach would be to fork archived GH repo for your PKE repo to add query-like features, such as scanning frontmatter or tags.

- Community discussions on extending mdBook (e.g., via preprocessors for custom features) are ongoing, but no full Dataview clone is under active open development as of mid-2025. Anyone interested in collaborating or forking extending mdBook should check Rust forums or GitHub issues for mdBook extensions.

For a comprehensive list of mdBook plugins, refer to the official third-party plugins wiki, though it doesn't highlight any exact Dataview matches. If none fit, building your own is feasible given mdBook's extensible architecture.

### Approaches to Building a Custom mdBook Dynamic Plugin
Here are several practical approaches to create Dataview-like functionality in mdBook for your PKE system. These build on mdBook's preprocessor system (which processes content before rendering) and can handle dynamic generation based on metadata, tags, or queries in your Markdown files. Your PKE repo appears to be a GitHub Pages-hosted mdBook site focused on knowledge management concepts, so these could integrate via custom chapters or automated builds.

#### 1. Custom Preprocessor with Query Syntax (Server-Side Build-Time Generation)
This is the most direct way to mimic Dataview: Create a preprocessor that scans your book's Markdown files, parses queries, and generates content during the `mdbook build` process.

- **Steps**:
  - Define a custom syntax in your Markdown, e.g., fenced code blocks like:
    ```
    ```pke-query
    TABLE title, tags, summary
    FROM folder:notes WHERE tags CONTAINS #project
    ```
    ```
  - Write the preprocessor in Rust (or any language, e.g., Python via a script) that:
    - Receives the book's JSON structure via stdin.
    - Scans all chapters for frontmatter (YAML metadata like tags, dates) or inline elements.
    - Parses the query (use libraries like `serde` for JSON/YAML, or `pest` for query parsing in Rust).
    - Queries the content (e.g., filter files by tags, folders, or properties).
    - Generates Markdown/HTML output (e.g., a table) and replaces the query block.
  - Configure in `book.toml`:
    ```
    [preprocessor.pke-dataview]
    command = "./target/release/mdbook-pke-dataview"  # Or path to your script
    ```
- **Pros**: Fully integrated, no runtime overhead; works offline.
- **Cons**: Build-time only (not live updates); requires recompiling for changes.
- **Tools/Libs**: In Rust, use `mdbook::preprocess` crate; for Python, parse JSON input and use `pandas` for querying data.
- **Extension for PKE**: Start by extracting metadata from your existing notes in the repo, then generate index pages dynamically.

#### 2. JavaScript-Based Client-Side Dynamics (Post-Render Manipulation)
For interactive queries without rebuilding the book each time, embed JavaScript to query and manipulate the DOM after the HTML is generated.

- **Steps**:
  - In your mdBook theme (customize `theme/index.hbs` or add JS via `additional-js` in `book.toml`), include a script that loads all page data (e.g., via a pre-generated JSON index of metadata).
  - Pre-build a metadata index: Use a script to scan Markdown files and output a `data.json` with entries like `{ "path": "notes/project.md", "tags": ["#project"], "summary": "..." }`.
  - In Markdown, add placeholders like `<div class="pke-query" data-query="FROM #project"></div>`.
  - JS code (e.g., with vanilla JS or a lib like DataTables) fetches the JSON, filters based on the query, and injects tables/lists.
  - Example JS snippet:
    ```javascript
    document.querySelectorAll('.pke-query').forEach(el => {
      const query = el.dataset.query;
      fetch('/data.json').then(res => res.json()).then(data => {
        // Filter data based on query logic
        const results = data.filter(item => item.tags.includes('#project'));
        // Generate and insert table HTML
        el.innerHTML = generateTable(results);
      });
    });
    ```
- **Pros**: Interactive (e.g., sortable tables); no full rebuild needed for minor changes.
- **Cons**: Requires JS enabled; heavier for large books; data must be static or pre-indexed.
- **Tools/Libs**: Use `lunr.js` for search indexing or `alasql` for SQL-like queries on JSON.
- **Extension for PKE**: This could add real-time filtering to your GitHub Pages site, enhancing knowledge navigation.

#### 3. Hybrid Pre-Build Scripting with External Tools
Run scripts before `mdbook build` to generate dynamic content, treating your Markdown as a database.

- **Steps**:
  - Use tools like `jq` (for JSON) or `awk` to process files, or a full script in Python/Node.js.
  - Example: A bash/Python script that:
    - Recursively scans `.md` files for frontmatter/tags.
    - Builds a database (e.g., SQLite or JSON).
    - Executes queries and outputs generated Markdown files (e.g., auto-create an "index.md" with tables).
  - Integrate via a Makefile or GitHub Actions workflow: `make generate && mdbook build`.
  - For queries, mimic Dataview with a custom DSL parsed by your script.
- **Pros**: Flexible; leverage existing tools (e.g., combine with `pandoc` for advanced processing).
- **Cons**: Adds build steps; not as seamless as a native plugin.
- **Tools/Libs**: Python with `frontmatter` lib for metadata; `sqlite3` for querying.
- **Extension for PKE**: Automate this in your repo's CI to regenerate views on push, keeping your knowledge base up-to-date.

#### 4. Integration with External Frameworks or Generators
Embed mdBook within a larger system for advanced dynamics, especially if your PKE evolves beyond static sites.

- **Steps**:
  - Use mdBook as a content source, but render via a dynamic framework like Next.js (with MDX for Markdown).
    - Example: Fork something like "MDNext" (a Next.js starter for MDX) to add query layers.
    - Parse mdBook output into a Next.js site, adding server-side querying.
  - Or, sync your Markdown to a tool like Obsidian (for Dataview) and export back, but this is roundabout.
  - For GitHub Pages, use Jekyll plugins if migrating, but stick to mdBook for Rust ecosystem benefits.
- **Pros**: Scales to full apps; adds features like search APIs.
- **Cons**: Increases complexity; may require rewriting parts of your PKE setup.
- **Tools/Libs**: Next.js with `next-mdx-remote`; or Rust alternatives like Leptos for web apps.
- **Extension for PKE**: If your system grows, this could turn your static book into a web app with user queries.

Start with the preprocessor approach for closest integration, as it's mdBook-native and aligns with your provided example. Test on a branch of your repo, and consider open-sourcing the plugin to attract contributors. If I need code snippets or help with implementation, all that I need to doe is provide more details to Grok, when I understand the specifics of what I need!