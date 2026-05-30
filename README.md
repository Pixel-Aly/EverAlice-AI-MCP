# EverAlice Studio MCP Server

AI-powered listing and creative workflow tools for Etsy sellers, digital product creators, and print-on-demand shops.

EverAlice Studio exposes a hosted MCP server with 14 tools for listing copy, product art, mockup planning, KDP copy, planner outlines, book outlines, image upscaling, background removal, and ad copy.

## MCP Endpoint

```text
https://kfdadgtwmcmgehstagbe.supabase.co/functions/v1/mcp-server
```

Transport: streamable HTTP

Protocol: MCP `2025-06-18`

## Tools

- `magic_lister_single` - Generate a platform-optimized listing for one product, with delivery ZIP download support when available.
- `magic_lister_bundle` - Generate a bundle listing, with delivery ZIP download support when available.
- `magic_lister_bulk` - Generate up to 10 listing sets in one call, with delivery ZIP download support when available.
- `ai_copywriter` - Generate short-form ecommerce copy.
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

Create an EverAlice API key from your EverAlice Studio account, then configure your MCP client with bearer-token authentication.

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

## Notes

The MCP Magic Lister tools generate structured marketplace listing output and can surface delivery package download links when the generated ZIP workflow is available for that product. For standalone image generation, mockup concepts, upscaling, and background removal, use the dedicated MCP tools such as `generate_image`, `generate_mockup_concept`, `upscale_image`, and `remove_background`.

The full EverAlice Studio web app includes additional end-to-end workflows for mockups, print exports, and delivery ZIP packages.

## Documentation

- [EverAlice Studio developer docs](https://everalice.studio/developers)
- [MCP manifest](https://everalice.studio/.well-known/mcp.json)
