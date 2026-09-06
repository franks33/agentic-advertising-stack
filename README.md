# The Agentic Advertising Stack

A curated map of the protocols, standards, and infrastructure that let AI agents plan, buy, sell, deliver, and measure advertising. Organized by layer, from the generic agent protocols at the bottom up through ad-specific protocols, sell-side and buy-side infrastructure, commerce, identity, and the publisher/content signals that decide what AI surfaces are allowed to monetize.

This list covers the infrastructure and standards layer. For MCP servers and tools that drive individual ad platforms (Google, Meta, TikTok, LinkedIn and so on), see [awesome-agentic-advertising](https://github.com/jshorwitz/awesome-agentic-advertising), which does that well and which this list does not try to duplicate.

**Disclosure.** I am a co-founder of [Adgentek](https://adgentek.ai), so read the Adgentek entries accordingly; each is marked *(disclosure: my company)*. Adgentek is a Founding Member of AdCP and a member of IAB and IAB Tech Lab. My aim is to cover every serious effort in the space on equal footing regardless of governing body.

**Last updated:** September 5, 2026. Pull requests welcome; see [Contributing](#contributing).

## Contents

1. [Foundation protocols](#1-foundation-protocols)
2. [Advertising protocols and standards bodies](#2-advertising-protocols-and-standards-bodies)
3. [Sell side: sales agents, ad servers, and adapters](#3-sell-side-sales-agents-ad-servers-and-adapters)
4. [Buy side: buying agents and orchestrators](#4-buy-side-buying-agents-and-orchestrators)
5. [First-party MCP servers from major ad platforms](#5-first-party-mcp-servers-from-major-ad-platforms)
6. [Registries, discovery, and adoption tracking](#6-registries-discovery-and-adoption-tracking)
7. [Agent identity and trust](#7-agent-identity-and-trust)
8. [Agentic commerce and payments](#8-agentic-commerce-and-payments)
9. [Publisher content, licensing, and AI-surface monetization](#9-publisher-content-licensing-and-ai-surface-monetization)
10. [Measurement and attribution](#10-measurement-and-attribution)
11. [Creative and provenance](#11-creative-and-provenance)
12. [Reading](#12-reading)
13. [Related lists](#13-related-lists)

---

## 1. Foundation protocols

The general-purpose agent protocols everything above them is built on.

- [Model Context Protocol (MCP)](https://github.com/modelcontextprotocol/modelcontextprotocol) - Agent-to-tool protocol originated by Anthropic, now under the Linux Foundation's Agentic AI Foundation. AdCP and AAMP both run over it. [Docs](https://modelcontextprotocol.io).
- [Agent2Agent (A2A)](https://github.com/a2aproject/A2A) - Agent-to-agent communication and task delegation, originated by Google, now Linux Foundation governed. AdCP supports it as a second transport.
- [WebMCP](https://github.com/webmachinelearning/webmcp) - Browser-native variant that lets web pages expose tools directly to agents. Relevant to on-page ad experiences agents interact with.
- [Agent Skills](https://github.com/agentskills/agentskills) - Specification for packaging reusable agent capabilities. The likely container for "ad buying as a skill" any agent can load.
- [AGENTS.md](https://github.com/agentsmd/agents.md) - Open format for guiding coding agents inside a repo; increasingly used as a general agent-instructions convention.
- [Agent Network Protocol (ANP)](https://github.com/agent-network-protocol/AgentNetworkProtocol) - Decentralized agent discovery and communication built on W3C DIDs. Early, but the DID approach is relevant to agent identity below.
- [Agentic AI Foundation (AAIF)](https://aaif.io) - The Linux Foundation home for MCP, A2A, AP2, UCP and related work, including an Agentic Commerce Working Group.

## 2. Advertising protocols and standards bodies

The ad-specific protocols and the organizations that govern them.

### AdCP (Ad Context Protocol), AgenticAdvertising.org

Open protocol for agents to discover, plan, buy, sell, and measure media. Published and governed by AgenticAdvertising.org (AAO). Current spec is 3.1, with a 3.2 preview available on the AAO site. Launched publicly October 15, 2025 with Yahoo, PubMatic, Optable, Scope3, Swivel and Triton Digital as founding members and 20-plus supporting companies.

- [AgenticAdvertising.org](https://agenticadvertising.org) - Standards body: membership, governance, certification (the Addie academy), registry.
- [AdCP spec and reference implementation](https://github.com/adcontextprotocol/adcp) - Docs and reference code. [Versioned docs](https://docs.adcontextprotocol.org).
- SDKs: [TypeScript](https://github.com/adcontextprotocol/adcp-client) (client and server), [Python](https://github.com/adcontextprotocol/adcp-client-python), [Go](https://github.com/adcontextprotocol/adcp-go), [Java](https://github.com/adcontextprotocol/adcp-sdk-java).
- [Reference creative agent](https://github.com/adcontextprotocol/creative-agent) and [reference signals agent](https://github.com/adcontextprotocol/signals-agent).
- [Registry API docs](https://docs.adcontextprotocol.org/dist/docs/3.1.2/registry) - Brand resolution, property lookup, agent discovery, and authorization validation (adagents.json and brand.json).

### AAMP (Agentic Advertising Management Protocols), IAB Tech Lab

IAB Tech Lab's umbrella initiative for agentic advertising, formally published March 16, 2026 across three pillars: Agentic Foundations, Agentic Protocols, and Trust and Transparency. AAMP 2.3 shipped July 30, 2026. Tech Lab has said it will "agentify" its existing standards (OpenRTB, ads.txt, sellers.json, VAST and others) under this umbrella and ship Agentic Protocol SDKs.

- [IAB Tech Lab agentic advertising hub](https://iabtechlab.com/standards/agentic-advertising-and-ai/) - Program overview and links.
- [AAMP hub repo](https://github.com/IABTechLab/AAMP) - Central repository linking every AAMP child repo.
- [Agentic Real-Time Framework (ARTF)](https://github.com/IABTechLab/agentic-real-time-framework) - How agents operate inside real-time bidding environments where responses are due in milliseconds.
- [Buyer agent](https://github.com/IABTechLab/buyer-agent) and [seller agent](https://github.com/IABTechLab/seller-agent) - Tech Lab reference agents.
- [Agentic Direct](https://github.com/IABTechLab/agentic-direct) - Direct-sold and guaranteed deals in an agentic workflow.
- [Agentic Audiences](https://github.com/IABTechLab/agentic-audiences) - Open standard originated by LiveRamp for how agents exchange user context.
- [Agentic Mobile](https://github.com/IABTechLab/agentic-mobile) - Mobile and in-app profile.
- [IAB agentic primitives](https://github.com/IABTechLab/iab-agentic-primitives) - Shared contract library: primitives, wire protocol, state machines.
- [Registry agent example](https://github.com/IABTechLab/registry-agent-example) - Example agent for Tech Lab's registry work.

### Other

- [Prebid Sales Agent](https://github.com/prebid/salesagent) - Prebid.org's media sales agent implementing the AdCP Media Buy protocol. The main open-source sell-side agent today.

## 3. Sell side: sales agents, ad servers, and adapters

Infrastructure that lets a publisher, AI surface, or SSP expose inventory to buying agents.

- [Prebid Sales Agent](https://github.com/prebid/salesagent) - Open-source AdCP sales agent from Prebid.org. Multi-tenant, with adapters to downstream ad servers.
- [IAB Tech Lab seller agent](https://github.com/IABTechLab/seller-agent) - AAMP reference seller.
- [Adgentek Agentic Ad Server and AdsMCP](https://adsmcp.ai) *(disclosure: my company)* - Ad server built for AI surfaces (chat assistants, answer engines, agents). AdsMCP is the MCP integration path into it, letting an AI surface or agent request and render ads over MCP. [Repo](https://github.com/adgentek/adsmcp).
- [Scope3 Storefronts](https://scope3.com) - Sell-side listings on Scope3's Interchange, discoverable to any buying agent that speaks AdCP.
- [AdCP reference creative agent](https://github.com/adcontextprotocol/creative-agent) - Creative generation and adaptation as a sell-side or third-party service in the AdCP flow.

## 4. Buy side: buying agents and orchestrators

Agents that translate a brief, budget, and guardrails into media decisions and transact with sell-side agents.

- [IAB Tech Lab buyer agent](https://github.com/IABTechLab/buyer-agent) - AAMP reference buyer.
- [Adgentek ORCA](https://adgentek.ai) *(disclosure: my company)* - Orchestrated Real-time Collaborative Agents. Buy-side platform that sits above the transaction layer and dispatches outcome agents to AdCP-compliant sell-side infrastructure. Not a DSP. Background: [The Two Paths of Agentic Media Buying](https://adgentek.ai/blog/two-paths-agentic-media-buying).
- [Scope3 Interchange](https://scope3.com/agentic-advertising/) - Agent-to-agent marketplace built on AdCP where buying agents discover, negotiate, and transact with sales, signals, creative, and governance agents. Connects into Claude and ChatGPT as a connector; [plugin repo](https://github.com/scope3data/interchange-plugin) and [TypeScript client](https://github.com/scope3data/agentic-client).
- [Guidance for Advertising Agents on AWS](https://github.com/aws-solutions-library-samples/guidance-for-advertising-agents-on-aws) - Amazon's sample multi-agent advertising stack on Bedrock AgentCore, including an AdCP MCP gateway.
- [Kochava StationOne](https://digiday.com/media-buying/ad-tech-briefing-iab-tech-lab-accelerates-push-to-make-agentic-ai-more-practical/) - Desktop orchestration layer connecting AI models and ad tech tools through API keys and MCP; its AAMP workspace was open-sourced with IAB Tech Lab in March 2026.

## 5. First-party MCP servers from major ad platforms

One inclusion rule: the MCP server is operated by a major ad platform (a walled garden or social/retail platform selling its own inventory) and gives third-party agents access to that platform's ad stack. This is the "walled gardens opening up" signal, and it is the one thing the registries do not capture. DSPs, SSPs, and other ad tech vendors belong in the registries in the next section, whether or not they ship an MCP server; community wrappers and marketing-tool connectors belong in [awesome-agentic-advertising](https://github.com/jshorwitz/awesome-agentic-advertising).

- [Amazon Ads MCP Server](https://advertising.amazon.com/library/news/amazon-ads-mcp-server-open-beta) - Open beta announced at IAB ALM, February 2, 2026. Amazon-hosted; bundles multi-step workflows (campaign launch, locale expansion, reporting) into tools. Full create, update, and delete.
- [Google Ads MCP](https://github.com/googleads/google-ads-mcp) - Google's official open-source MCP server for the Google Ads API, released October 2025. Read-only diagnostics and GAQL queries.
- [Meta Ads MCP Server](https://developers.facebook.com/documentation/ads-commerce/ads-ai-connectors/ads-mcp-server/ads-mcp-server-get-started) - Meta Ads AI Connectors, launched April 29, 2026, at `mcp.facebook.com/ads`. Performance reporting, campaign and catalog management, and signal diagnostics; per-app Read or Manage scope, with writes landing paused. [Meta MCP overview](https://developers.facebook.com/documentation/mcp).
- [Microsoft Advertising MCP Server](https://about.ads.microsoft.com/en/solutions/technology/mcp-server) - First-party server launched June 17, 2026 as an open pilot. Read-only campaign data inside Copilot, Claude, and other assistants.
- Pinterest MCP - Announced June 17, 2026 in alpha with agency partners including PMG, Pacvue, and Dentsu; read-only. No public developer docs yet; see [PPC Land](https://ppc.land/pinterests-mcp-server-and-ask-pinterest-app-rewrite-the-discovery-playbook/).
- [Snapchat Ads MCP Server](https://developers.snap.com/marketing-api/Ads-MCP/Introduction) - Snap-hosted server at `mcp.snapchat.com/ads`, launched August 3, 2026, supporting Claude, ChatGPT, Codex, and Gemini. Read-only at launch; Organization Admins authorize each agent separately, with write access to follow as a per-agent grant. [Announcement](https://forbusiness.snapchat.com/blog/snapchat-ads-mcp).
- [TikTok for Business MCP Server](https://business-api.tiktok.com/portal/docs/tiktok-ads-mcp-server/v1.3) - TikTok's official MCP bridge for connecting AI agents to the TikTok Ads platform, including campaign creation and bid adjustments.
- [X Ads MCP](https://docs.x.com/x-ads-api/mcp) - Official remote MCP server built into X's Ads API gateway at `ads-api.x.com/mcp`. 23 tools spanning reads, analytics, targeting search, and writes; the user's own OAuth2 token scopes access, and every campaign or line item is created paused.

## 6. Registries, discovery, and adoption tracking

How agents find each other, prove who is authorized to sell what, and how the ecosystem tracks who is actually live.

- [AAO Agent Registry](https://agenticadvertising.org/registry/) - Public registry of sales, creative, and signals agents implementing AdCP. [API reference](https://docs.adcontextprotocol.org/dist/docs/3.1.2/registry). [Tools and standards page](https://agenticadvertising.org/registry/tools).
- [IAB Tech Lab Agent & MCP Server Registry](https://registry.iabtechlab.ai/) - The Trust and Transparency pillar of AAMP. Registers MCP and A2A agents with category (identity, clean room, DSP/SSP, consent, measurement), capabilities, maturity, verification, and endorsements; browsable without a login, registration through the Tools Portal. Launched March 2026; Amazon, Optable, Dstillery and others among early entries. Reference companion: [registry-agent-example](https://github.com/IABTechLab/registry-agent-example).
- [adagents.json builder and validator](https://agenticadvertising.org/adagents/builder) - Create and validate the manifest a publisher uses to declare authorized sales agents.
- [adcontextprotocol/registry](https://github.com/adcontextprotocol/registry) - Registry source.
- [AdCP Ecosystem Tracker (No Fluff Advisory)](https://nofluffadvisory.com/adcp-registry/) - Independent, dated view of the registry with daily endpoint probes showing which registered agents actually answer discovery.
- [MCP Registry](https://github.com/modelcontextprotocol/registry) - The community-driven registry for MCP servers generally. Ad tech servers should appear here as well as in the two advertising registries.
- [GitHub topic: agentic-advertising](https://github.com/topics/agentic-advertising) - Everything tagged on GitHub.

## 7. Agent identity and trust

The thin layer between "a legitimate buying agent" and "invalid traffic." Mostly borrowed from the commerce and bot-management worlds so far; ad-specific attestation is still open ground.

- [Web Bot Auth](https://github.com/cloudflare/web-bot-auth) - Cloudflare-led IETF drafts (built on RFC 9421 HTTP Message Signatures) for agents to cryptographically sign requests so the receiving side can verify identity. Still an individual Internet-Draft as of August 2026, but verified in production by Cloudflare and adopted by major agent operators. [Cloudflare docs](https://developers.cloudflare.com/bots/reference/bot-verification/web-bot-auth/).
- [Visa Trusted Agent Protocol (TAP)](https://github.com/visa/trusted-agent-protocol) - Visa's agent-to-merchant trust framework using HTTP Message Signatures (RFC 9421), built on Web Bot Auth. Announced October 2025.
- Mastercard Agent Pay / Verifiable Intent - Agentic Tokens extending MDES so verified agents can transact on a consumer's behalf; the Verifiable Intent framework was contributed to the FIDO Alliance alongside AP2 in April 2026. See the [AAIF explainer](https://aaif.io/blog/how-does-agentic-commerce-work).
- [Agent Payments Protocol (AP2)](https://github.com/google-agentic-commerce/AP2) - Signed Intent, Cart, and Payment mandates (W3C Verifiable Credentials) proving what a user authorized an agent to do. Google contributed AP2 to the FIDO Alliance in April 2026.
- [Agent Network Protocol (ANP)](https://github.com/agent-network-protocol/AgentNetworkProtocol) - DID-based agent identity, listed again here for the identity angle.

## 8. Agentic commerce and payments

Where the ad converts. When the agent that saw the ad is the agent that checks out, outcome measurement runs through these protocols rather than pixels.

- [Universal Commerce Protocol (UCP)](https://github.com/Universal-Commerce-Protocol/ucp) - Google and Shopify led; discovery, cart, and checkout primitives. Under Linux Foundation governance; Amazon, Meta, Microsoft, Salesforce and Stripe joined the tech council in April 2026.
- [Agentic Commerce Protocol (ACP)](https://github.com/agentic-commerce-protocol/agentic-commerce-protocol) - OpenAI and Stripe; originally in-chat checkout, refocused on product discovery in March 2026.
- [Agent Payments Protocol (AP2)](https://github.com/google-agentic-commerce/AP2) - Payment authorization layer (see Agent identity and trust above).
- [x402](https://github.com/coinbase/x402) - Coinbase's HTTP-native payments protocol reviving the 402 status code for machine-to-machine stablecoin payments.
- [Machine Payments Protocol (MPP)](https://mpp.dev) - Stripe and Tempo's open standard for agent payments over HTTP 402, launched March 18, 2026, with stablecoin and card support from day one; Visa extended it to card rails. [Specs](https://github.com/tempoxyz/mpp-specs), [Stripe announcement](https://stripe.com/blog/machine-payments-protocol).
- [AAIF Agentic Commerce Working Group](https://aaif.io/blog/how-does-agentic-commerce-work) - Where the commerce protocols are being coordinated.

## 9. Publisher content, licensing, and AI-surface monetization

The standards deciding whether AI surfaces pay for the content they use, monetize it with ads, or both.

- [Really Simple Licensing (RSL)](https://rslstandard.org) - Machine-readable licensing terms in robots.txt and feeds: free, attribution, subscription, pay-per-crawl, pay-per-inference. Launched September 10, 2025 with Reddit, Yahoo, People Inc., Medium and others. [Repo](https://github.com/rslstandard/rsl).
- [Content Monetization Protocols (CoMP)](https://github.com/IABTechLab/CoMP) - IAB Tech Lab protocol for establishing commercial terms between publishers and AI systems before content is accessed. Version 1.0 released for public comment March 23, 2026.
- [Cloudflare Content Signals](https://blog.cloudflare.com/agent-readiness/) - robots.txt directive (ai-train, ai-input, search) declaring what AI may do with content. Submitted to the IETF AIPREF working group.
- [Cloudflare Pay Per Crawl](https://developers.cloudflare.com/ai-audit/features/pay-per-crawl/use-pay-per-crawl-as-ai-owner/crawl-pages) - HTTP 402 based charging for crawler access, gated on Web Bot Auth.
- [llms.txt](https://github.com/AnswerDotAI/llms-txt) - Convention for telling language models how to use a site.
- [NLWeb](https://github.com/nlweb-ai/NLWeb) - Microsoft's reference implementation for natural-language interfaces to websites, exposed over MCP.
- SPUR Telemetry - Emerging standard for measuring how publisher content is used inside AI systems. See the [INMA overview](https://www.inma.org/blogs/product-initiative/post.cfm/comp-rsl-and-spur-3-standards-every-publisher-should-understand).

## 10. Measurement and attribution

The open problem. Clicks, UTMs, and referrers do not survive an AI intermediary, and nobody yet agrees who gets credit when an agent reads, compares, and buys.

- [IAB AI advertising measurement framework](https://digiday.com/media/the-iab-is-developing-a-framework-to-tackle-ai-advertising-measurement/) - In development by IAB (the trade group, distinct from Tech Lab) with a working group of platforms, publishers, agencies, measurement vendors, and brands; scheduled for release November 12, 2026. Aims to separate AI's awareness-level influence from its role in the actual decision.
- [AAO Registry measurement agents](https://docs.adcontextprotocol.org/dist/docs/3.1.2/registry) - The AdCP registry crawls measurement agents' capabilities and exposes them as a queryable metric catalog (attention, viewability, MRC accreditation filters).
- [IAB Tech Lab measurement standards being agentified](https://iabtechlab.com/standards/agentic-advertising-and-ai/) - OMID / OM SDK for exposure events and ECAPI for outcome events are on Tech Lab's list of standards to extend for agents under AAMP.
- SPUR Telemetry - Measurement of how publisher content is used inside AI systems; see the publisher section above.

## 11. Creative and provenance

- [C2PA](https://c2pa.org) - Content Credentials for provenance of AI-generated and edited creative. [Rust SDK](https://github.com/contentauth/c2pa-rs).
- [IAB AI Transparency and Disclosure Framework](https://www.prnewswire.com/news-releases/iab-releases-industrys-first-ai-transparency-and-disclosure-framework-to-guide-responsible-advertising-in-a-generative-ai-landscape-302661683.html) - Released January 15, 2026. Risk-based, two-layer disclosure model for AI in advertising, including synthetic avatars and conversational agents in ads.
- [AdCP reference creative agent](https://github.com/adcontextprotocol/creative-agent) - How creative generation and adaptation participate in the AdCP flow.

## 12. Reading

Explainers and reporting worth the time, most recent first.

- [Web Bot Auth: how signed agents change who gets to crawl](https://crawlbase.com/blog/web-bot-auth-signed-agents/) - Crawlbase, late August 2026. Where the IETF drafts actually stand (still individual drafts as of August 18) versus what Cloudflare and the large agent operators already enforce in production.
- [AI advertising's measurement problem is really a governance problem](https://digiday.com/media-buying/ad-tech-briefing-ai-advertisings-measurement-problem-is-really-a-governance-problem/) - Digiday, August 2026. Who controls the signals that prove an agent was influenced.
- [Butler/Till extends agentic media buying tests into audio with iHeartMedia](https://digiday.com/media-buying/butler-till-extends-agentic-media-buying-tests-into-audio-with-iheartmedia/) - Digiday, August 20, 2026. A matched pair of buyer and seller agents over an MCP server, roughly $10,000 in spend, 42% lower CPMs than the client's direct-buy benchmark; broadcast radio to follow.
- [How does agentic commerce work?](https://aaif.io/blog/how-does-agentic-commerce-work) - AAIF, August 2026. The commerce protocol stack from the body that governs most of it.
- [AdCP 3.1 vs. IAB Tech Lab AAMP 2.3: A Complete Comparison](https://adgentek.ai/blog/adcp-vs-aamp) - Adgentek, August 4, 2026 *(disclosure: my company)*. Clause-level comparison of the two protocols and what the overlap costs operators.
- [What are AdCP and AAMP?](https://www.fluency.inc/blog/what-are-adcp-aamp-agentic-advertising-protocol-standards) - Fluency, August 2026. Clear on the campaign-layer vs. real-time-layer distinction.
- [MCP vs A2A vs AP2 vs UCP vs ACP](https://stellagent.ai/insights/mcp-vs-a2a-vs-ap2-protocol-comparison) - Stellagent, August 1, 2026. Five-layer map of the commerce and trust protocols.
- [MCP forces ad tech to rebuild agent servers as sessions disappear](https://ppc.land/mcp-forces-ad-tech-to-rebuild-agent-servers-as-sessions-disappear/) - PPC Land, July 31, 2026. What the 2026-07-28 MCP spec means for every ad tech MCP server, plus the best running list of who has shipped one.
- [AdCP and AAMP: the new infrastructure of agentic media buying](https://star.global/posts/agentic-advertising-standards-adcp-and-aamp/) - Star Global, July 11, 2026.
- [CoMP, RSL, and SPUR: three standards every publisher should understand](https://www.inma.org/blogs/product-initiative/post.cfm/comp-rsl-and-spur-3-standards-every-publisher-should-understand) - INMA, July 7, 2026.
- [A guide to the new, wide world of agentic advertising and commerce protocols](https://tech.yahoo.com/ai/meta-ai/articles/guide-wide-world-agentic-advertising-100000253.html) - Yahoo Tech, May 28, 2026.
- [The Agent Stack 2026](https://sanbi.ai/blog/agent-stack-protocols-2026) - Sanbi, May 11, 2026. Broad survey including WebMCP, ANP, x402, and llms.txt.
- [The Ad Context Protocol aims to make sense of agentic ad demand](https://www.adexchanger.com/marketers/the-ad-context-protocol-aims-to-make-sense-of-agentic-ad-demand/) - AdExchanger, October 15, 2025. The launch coverage.

## 13. Related lists

- [awesome-agentic-advertising](https://github.com/jshorwitz/awesome-agentic-advertising) - Ad platform MCP servers, creative generation tools, conversion APIs.
- [awesome-agentic-payments](https://github.com/bitrefill/awesome-agentic-payments) - Deeper coverage of the payments layer: ACP, UCP, AP2, TAP, MPP, x402, and the SDKs around them.
- [GitHub topic: agentic-advertising](https://github.com/topics/agentic-advertising)

---

## Contributing

Open a pull request. One entry per line, in the form `[Name](url) - one sentence on what it is and why it matters.` Entries need a live, public artifact: a spec, a repo, an API, or a shipping product. Announcements without an artifact go in Reading. If you are adding your own company, say so inline the way the Adgentek entries do.

## License

[CC0 1.0 Universal](LICENSE). Copy, fork, and reuse freely.
