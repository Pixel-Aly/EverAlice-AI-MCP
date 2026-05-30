# EverAlice Studio MCP Server

[![Website](https://img.shields.io/badge/Website-everalice.studio-purple)](https://everalice.studio)
[![Developer Docs](https://img.shields.io/badge/Docs-MCP%20Developers-blue)](https://everalice.studio/developers)
[![MCP Manifest](https://img.shields.io/badge/MCP-Manifest-green)](https://everalice.studio/.well-known/mcp.json)
[![Transport](https://img.shields.io/badge/Transport-Streamable%20HTTP-orange)](#mcp-endpoint)

AI-powered listing and creative workflow tools for Etsy sellers, digital product creators, and print-on-demand shops.

EverAlice Studio exposes a hosted MCP server with 15 tools for listing copy, full listing packs with ZIP download links, product art, mockup planning, KDP copy, planner outlines, book outlines, image upscaling, background removal, and ad copy.

The headline tool is `magic_lister_pack`: it runs the Magic Lister workflow server-side, creates marketplace listing copy, generates a hero product image and lifestyle mockups, packages the result into a ZIP, and returns signed download URLs that an AI assistant can hand back to the user.

Use EverAlice from Claude Desktop, Codex, ChatGPT-compatible MCP clients, n8n workflows, and other automation tools to create Etsy listings, digital download products, KDP assets, printable wall art, product mockups, Pinterest ad copy, and SEO-friendly marketplace content.

## Quick Links

- Website: [everalice.studio](https://everalice.studio)
- Developer docs: [everalice.studio/developers](https://everalice.studio/developers)
- MCP manifest: [everalice.studio/.well-known/mcp.json](https://everalice.studio/.well-known/mcp.json)
- Account settings and API keys: [everalice.studio/settings](https://everalice.studio/settings)

## What Is EverAlice Studio?

[EverAlice Studio](https://everalice.studio) is an AI Etsy listing generator and digital product workflow platform for sellers who create printables, wall art, planners, journals, templates, POD products, and other downloadable products.

The EverAlice MCP server lets AI assistants call EverAlice tools directly, so creators can move from a plain-English product idea to listing copy, mockup concepts, generated product art, and full listing packs without leaving their assistant or automation workflow.

## Who Is This For?

- Etsy sellers creating digital downloads, printables, wall art, planners, journals, stickers, templates, and POD products.
- Digital product creators selling on Etsy, Shopify, Gumroad, Payhip, Creative Market, or Amazon KDP.
- Designers who want AI product images, background removal, upscaling, and mockup planning in one workflow.
- Automation builders connecting Claude, Codex, ChatGPT, n8n, or other MCP clients to an ecommerce content pipeline.
- Small shops that want consistent brand voice, marketplace SEO, and repeatable listing workflows.

## MCP Endpoint

```text
https://kfdadgtwmcmgehstagbe.supabase.co/functions/v1/mcp-server
```

Transport: streamable HTTP

Protocol: MCP `2025-06-18`

## Tools

- `magic_lister_single` - Generate platform-optimized listing copy for one product.
- `magic_lister_bundle` - Generate listing copy for a bundle of products.
- `magic_lister_bulk` - Generate up to 10 listing copy sets in one call.
- `ai_copywriter` - Generate short-form ecommerce copy.
- `magic_lister_pack` - Generate listing copy, a hero product image, lifestyle mockups, and a signed ZIP download URL.
- `generate_image` - Generate product art, posters, clipart, wallpapers, or listing photos.
- `upscale_image` - Upscale an existing image to a sharper print-ready PNG.
- `remove_background` - Remove an image background and return a transparent PNG.
- `generate_greeting_card` - Generate greeting card copy and design directions.
- `generate_kdp_cover_copy` - Generate Amazon KDP cover copy and category suggestions.
- `generate_planner_outline` - Generate a structured digital planner outline.
- `generate_printable_idea` - Generate a printable product concept.
- `generate_book_outline` - Generate a chapter-by-chapter book outline.
- `generate_mockup_concept` - Generate lifestyle mockup scene briefs.
- `generate_ad_copy` - Generate Pinterest, Facebook, Instagram, or short promo copy.

## Setup

Create an EverAlice Studio account, generate an API key, then configure your MCP client with bearer-token authentication.

### Create an EverAlice Account

1. Sign up at [everalice.studio](https://everalice.studio).
2. Open [EverAlice Studio settings](https://everalice.studio/settings).
3. Create or copy your MCP/API access key.
4. Store the key in your MCP client configuration or in an environment variable such as `EVERALICE_MCP_API_KEY`.

EverAlice offers a free Starter plan with limited AI usage and paid plans with monthly AI credits. Credit packs are also available for additional usage. See [EverAlice Studio pricing and account options](https://everalice.studio/developers) for current plan details.

### Claude Desktop

Add this to your Claude Desktop config:

```json
{
  "mcpServers": {
    "everalice": {
      "url": "https://kfdadgtwmcmgehstagbe.supabase.co/functions/v1/mcp-server",
      "headers": {
        "Authorization": "Bearer YOUR_KEY_HERE"
      }
    }
  }
}
```

### Codex CLI

```bash
codex mcp add everalice-studio \
  --url https://kfdadgtwmcmgehstagbe.supabase.co/functions/v1/mcp-server \
  --bearer-token-env-var EVERALICE_MCP_API_KEY
```

Set `EVERALICE_MCP_API_KEY` to your EverAlice API key before starting Codex.

## Example Prompts

Once connected to an MCP client, try prompts like:

```text
Use EverAlice to create a full Magic Lister pack for a printable ADHD wall art poster. Make 4 mockups and return the ZIP link.
```

```text
Generate an Etsy listing for a cozy fall digital planner. Include SEO title, tags, description, bullets, target audience, and category.
```

```text
Create three lifestyle mockup concepts for a minimalist kitchen wall art printable.
```

```text
Write Pinterest pin copy and Instagram ad variants for a printable homeschool chore chart bundle.
```

## Magic Lister Pack

`magic_lister_pack` is the MCP equivalent of running the full Magic Lister workflow inside EverAlice Studio.

It accepts:

- `product_description` - Plain-English product brief.
- `platform` - `etsy`, `shopify`, `gumroad`, `creative-market`, `amazon-kdp`, or `payhip`.
- `brand_name` - Optional brand/shop name.
- `keywords_to_include` - Optional SEO seed keywords.
- `mockup_count` - Number of lifestyle mockups to generate, from 0 to 6.
- `aspect` - `square`, `portrait`, or `landscape`.

It returns:

- `listing` - Marketplace-ready title, tags, description, bullet points, target audience, and category.
- `hero_image_base64` - Generated hero product image.
- `mockup_urls` - Signed URLs for generated mockups.
- `zip_url` - Signed ZIP download URL, valid for 7 days.
- `credits_used` - Total credits used for the run.

## Why Use This MCP Server?

- Etsy-tuned SEO for marketplace titles, tags, descriptions, and category fit.
- Brand consistency through EverAlice Studio account context where available.
- One EverAlice credit pool across Claude, Codex, ChatGPT, n8n, and other MCP clients.
- Full pack delivery through signed URLs, so AI assistants can return a clickable ZIP link instead of just text.
- Purpose-built digital product workflows for Etsy listing generation, AI mockups, printable products, Amazon KDP books, planners, journals, ads, and ecommerce copy.

For standalone image generation, mockup concepts, upscaling, and background removal, use the dedicated MCP tools such as `generate_image`, `generate_mockup_concept`, `upscale_image`, and `remove_background`.

## Common Use Cases

- Generate a complete Etsy listing from a product idea.
- Create SEO titles, tags, descriptions, bullets, categories, and target audience copy.
- Generate a full Magic Lister pack with product images, mockups, and a signed ZIP download link.
- Brainstorm new printable products, planner concepts, book outlines, greeting cards, and KDP cover copy.
- Create Pinterest pin copy, Instagram/Facebook ad variants, and short promotional copy.
- Upscale product artwork or remove backgrounds for cleaner listing images.

## Security & Privacy

- Do not commit EverAlice API keys to GitHub.
- Use environment variables or your MCP client's secret storage for bearer tokens.
- The MCP server requires authenticated requests with an EverAlice API key.
- Signed ZIP and mockup URLs are intended for generated delivery assets and should be treated as private download links.
- This repository contains setup docs and public endpoint metadata only; it does not contain the hosted server source code or any user secrets.

## Registry Notes

This repository is intended to give MCP directories and tooling a stable public URL for the hosted EverAlice Studio MCP server. The server is hosted by EverAlice Studio and is accessed over streamable HTTP with bearer-token authentication.

Suggested GitHub topics:

```text
mcp, mcp-server, etsy, etsy-seller-tools, ai-tools, digital-products, print-on-demand, kdp, n8n, ecommerce, product-listings, mockups
```

## Related Keywords

EverAlice Studio, EverAlice AI, MCP server, Etsy listing generator, AI Etsy tool, Etsy SEO generator, digital product seller tools, printable product generator, AI mockup generator, product listing copywriter, Amazon KDP AI tools, planner outline generator, wall art listing generator, Gumroad product listing, Shopify product copy, Creative Market listing, Payhip digital products, n8n MCP automation.

## Documentation

- [EverAlice Studio developer docs](https://everalice.studio/developers)
- [MCP manifest](https://everalice.studio/.well-known/mcp.json)
