# Awesome-Javascript-Runtimes

# Top JavaScript Runtimes Ecosystem

**Curated List of SaaS Products & Open-Source GitHub Projects**  
*Focused on Server-Side Execution, Edge Deployment & Self-Hosted JavaScript Engines*  
**Last updated: October 2026**

This repository tracks notable **SaaS platforms** and **open-source projects** for **JavaScript Runtimes**. These tools execute JavaScript outside the browser—powering servers, CLIs, serverless functions, and edge workers—with varying trade-offs in compatibility, security, performance, and ecosystem maturity.

**Examples** include Node.js, Deno, Bun, AWS Lambda, Google Cloud Run, Vercel, and Cloudflare Workers (the category leaders).

**Open-source emphasis**: This section is heavily expanded with every major active project for self-hosting, avoiding platform lock-in, and running JavaScript on your own infrastructure—ideal for teams that need control over execution environments, data residency, and runtime behavior. The open-source landscape is anchored by **Node.js** (the ecosystem standard with the broadest compatibility), **Deno** (the security-first runtime with native TypeScript and web standards), and **Bun** (the performance-focused drop-in replacement), with **workerd** (Cloudflare's edge runtime) and **LLRT** (AWS's low-latency runtime) serving specialized deployment targets.

Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.

## Table of Contents
- [SaaS/Hosted Platforms](#saas-hosted-platforms)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## SaaS/Hosted Platforms

- **[AWS Lambda (Node.js Runtime)](https://aws.amazon.com/lambda/)**  
  Serverless compute with official Node.js runtime support. Pay-per-invocation with generous free tier. **Cold start advantage**: Node.js remains the most mature Lambda runtime, though Bun's faster startup is relevant if using custom runtimes. Best for event-driven workloads already in the AWS ecosystem.

- **[Google Cloud Run](https://cloud.google.com/run)**  
  Serverless container platform supporting any Node.js application. **Pricing**: free tier includes 2 million requests/month; pay only for compute time used . Best for containerized Node.js apps wanting serverless scaling without vendor-specific runtime constraints.

- **[Vercel](https://vercel.com/)**  
  Frontend cloud with serverless functions optimized for Next.js and other frameworks. **Pricing**: Pro $20/developer/month with usage credit; Active CPU billing skips time spent waiting on I/O . Best for frontend-heavy applications where deployment simplicity matters.

- **[Render](https://render.com/)**  
  Unified platform for web services, databases, and background workers. **Pricing**: Pro workspace $25/month with unlimited seats; instances from $7/month . Private networking included on all plans, keeping services and databases on the same network. Best for teams wanting simpler pricing and integrated database hosting.

- **[Fly.io](https://fly.io/)**  
  Edge-deployed containers with global anycast networking. Best for applications needing geographic distribution without managing regions manually.

- **[Railway](https://railway.app/)**  
  Developer-friendly platform with infrastructure-as-code via `railway.json`. Best for quick deployments and prototypes where DX matters more than enterprise features.

- **[Deno Deploy](https://deno.com/deploy)**  
  Managed edge runtime for Deno applications. **Important transition**: Deploy Classic shut down July 20, 2026; projects must migrate to the new Deploy platform, which has fewer regions and no queue support . Best for Deno-native applications wanting edge deployment without self-hosting.

## Open-Source GitHub Projects

- **[Node.js](https://github.com/nodejs/node)**  
  **The ecosystem standard.** Native npm support, the largest package ecosystem, and the broadest native add-on compatibility . **Recent improvements**: Node 22–25 closed many performance gaps; Node 25's Buffer optimization processes large files 78% faster . **Native TypeScript type stripping** is now available, reducing build-step friction . **Trade-offs**: full system access by default (no permission model unless opting into `--permission`); toolchain must be assembled from separate packages (bundler, transpiler, test runner, linter) . Best for production systems requiring long-term stability, native module compatibility, and the widest ecosystem support.

- **[Deno](https://github.com/denoland/deno)**  
  **The security-first runtime.** **Deny-by-default permission model**: code cannot read files, open network connections, or access environment variables without explicit flags—structurally harder for supply chain attacks to exfiltrate data . **Native TypeScript** (no build step), web-standard APIs (`fetch`, `Request`, `Response`, `Web Streams`), and built-in tooling (`deno fmt`, `deno lint`, `deno test`, `deno check`) . **npm compatibility**: 98%+ of packages via `npm:` specifiers; Deno 2.8+ passes 75%+ of Node's own test suite . **Trade-offs**: packages relying on native bindings or internal Node plumbing may break; ecosystem gravity still favors Node . Best for security-sensitive applications, edge functions, and teams wanting a batteries-included toolchain.

- **[Bun](https://github.com/oven-sh/bun)**  
  **The performance-focused drop-in replacement.** Single binary combines runtime, package manager, bundler, test runner, and script runner—TypeScript and JSX run directly with no configuration . **Performance**: fastest cold starts (~31ms vs Node's ~142ms in one serverless measurement); usually highest HTTP throughput . **Install speed**: `bun install` is 10–30x faster than npm . **Node compatibility**: implements `node:` APIs deliberately so existing projects run unmodified, with gaps concentrated in native add-ons and edge-case stream/cluster behavior . **Status note**: Rust rewrite is experimental (99.8% test compatibility on Linux x64); current stable releases remain Zig-based . Best for greenfield projects, CLIs, serverless functions where cold start matters, and teams wanting consolidated tooling.

- **[workerd](https://github.com/cloudflare/workerd)**  
  Cloudflare's JavaScript/Wasm runtime for Workers. The open-source core of Cloudflare Workers, enabling self-hosted edge-like execution. Best for teams wanting Cloudflare Workers' V8 isolate model without vendor lock-in.

- **[LLRT (Low Latency Runtime)](https://github.com/awslabs/llrt)**  
  AWS's lightweight JavaScript runtime optimized for serverless. Uses QuickJS instead of V8, producing a small binary (~2.5MB) with fast startup. Best for Lambda functions where cold start and memory footprint are critical.

### Additional Strong Open-Source Options

- **WasmEdge** — High-performance WebAssembly runtime with JavaScript support. Best for edge and embedded scenarios where Wasm is preferred over V8 isolates .
- **txiki.js** — Small, modern JavaScript runtime based on QuickJS. Best for embedded and resource-constrained environments .
- **JerryScript** — JavaScript engine for IoT devices with limited memory. Best for microcontrollers and embedded systems .
- **Frameworks for building custom systems**: Use **Node.js** for production stability and ecosystem breadth. Choose **Deno** for security-critical applications and TypeScript-native workflows. Use **Bun** for performance-sensitive serverless and CLI tools. Deploy **workerd** or **LLRT** when edge or serverless latency is the primary constraint.

## How to Contribute

1. Fork the repo.
2. Add/edit entries in `README.md` (follow existing format).
3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.
4. Submit PR with a short explanation.

Star the repo if you find it useful!

## Disclaimer

- This is a **community-curated** list — not exhaustive and not an endorsement.
- **Runtime performance benchmarks are highly context-dependent**: published 2026 figures for the same runtimes disagree by 2–3x depending on hardware, framework, and test type . The framework architecture (e.g., Elysia vs Express) often matters more than the runtime .
- **"Node compatible" has limits**: Deno and Bun both claim high npm compatibility, but native add-ons and packages reaching into Node internals can break. Run your full test suite before migrating .
- **Deno Deploy Classic is shut down**: projects must migrate to the new Deploy platform; queues are not supported .
- **Bun's Rust rewrite is not production-default**: current stable releases remain Zig-based; treat the Rust work as a reliability roadmap, not something to wait for .

---

**Made for backend engineers, platform teams, and developers choosing an execution environment for JavaScript.**  
Let's make JavaScript runtimes more open, appropriately scoped, and understandable.
