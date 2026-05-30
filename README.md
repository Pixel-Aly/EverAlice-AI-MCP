# EverAlice Studio MCP Server

AI-powered listing and creative workflow tools for Etsy sellers, digital product creators, and print-on-demand shops.

EverAlice Studio exposes a hosted MCP server with 15 tools for listing copy, full listing packs with ZIP download links, product art, mockup planning, KDP copy, planner outlines, book outlines, image upscaling, background removal, and ad copy.

The headline tool is `magic_lister_pack`: it runs the Magic Lister workflow server-side, creates marketplace listing copy, generates a hero product image and lifestyle mockups, packages the result into a ZIP, and returns signed download URLs that an AI assistant can hand back to the user.

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

EverAlice offers a free Starter plan with limited AI usage and paid plans with monthly AI credits. Credit packs are also available for additional usage.

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

For standalone image generation, mockup concepts, upscaling, and background removal, use the dedicated MCP tools such as `generate_image`, `generate_mockup_concept`, `upscale_image`, and `remove_background`.

## Documentation

- [EverAlice Studio developer docs](https://everalice.studio/developers)
- [MCP manifest](https://everalice.studio/.well-known/mcp.json)
