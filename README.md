# Anteos MCP Server

> Book medical appointments with French doctors directly from your AI agent.

[![MCP Registry](https://img.shields.io/badge/MCP_Registry-active-green)](https://registry.modelcontextprotocol.io/servers/io.github.Anteos-Health%2Fanteos-booking)
[![Protocol](https://img.shields.io/badge/MCP-2025--11--25-blue)](https://modelcontextprotocol.io)

## Overview

The Anteos MCP Server lets AI agents search for doctors, check availability, book appointments, and manage cancellations — all confirmed in real-time in the doctor's calendar.

**Endpoint:** `https://anteoshealth.com/mcp`  
**Transport:** `streamable-http`  
**Full docs:** [anteoshealth.com/docs/mcp](https://anteoshealth.com/docs/mcp)

## Available Tools

| Tool | Description |
|---|---|
| `search_doctors` | Search doctors by specialty and/or city, with optional availability filter |
| `get_doctor_profile` | Get full profile: coverage, languages, reviews, and 7-day availability |
| `find_next_available` | Find next available slots over a period, filtered by specialty and/or city |
| `get_available_slots` | Get available time slots for a doctor on a specific date |
| `book_appointment` | Book a confirmed appointment, immediately added to the doctor's calendar |
| `get_appointment` | Retrieve appointment details and status (requires appointment token) |
| `cancel_appointment` | Cancel an existing appointment (requires appointment token) |
| `reschedule_appointment` | Atomically reschedule an appointment to a new date and time |
| `resend_appointment_token` | Re-send the appointment management link to the patient's email |
| `list_my_appointments` | List appointments created by this partner key, with status filtering |

## Quick Start

### AI Agents (Cursor / Claude / Cline)

Add to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "anteos": {
      "url": "https://anteoshealth.com/mcp",
      "headers": {
        "Authorization": "Bearer anteos_mcp_VOTRE_CLE"
      }
    }
  }
}
```

### curl

```bash
# List available tools
curl -X POST https://anteoshealth.com/mcp \
  -H "Authorization: Bearer anteos_mcp_VOTRE_CLE" \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list","params":{}}'

# Search doctors
curl -X POST https://anteoshealth.com/mcp \
  -H "Authorization: Bearer anteos_mcp_VOTRE_CLE" \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":2,"method":"tools/call","params":{"name":"search_doctors","arguments":{"specialty":"cardiologue","city":"Paris"}}}'

# Find next available slots
curl -X POST https://anteoshealth.com/mcp \
  -H "Authorization: Bearer anteos_mcp_VOTRE_CLE" \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":3,"method":"tools/call","params":{"name":"find_next_available","arguments":{"from_date":"2026-05-10","specialty":"cardiologue","city":"Paris"}}}'
```

## Authentication

All requests require a partner API key in the `Authorization` header:

```
Authorization: Bearer anteos_mcp_<your_key>
```

**To get a key:** Contact [luc.dufour@anteoshealth.com](mailto:luc.dufour@anteoshealth.com)

## Registry

Published on the official MCP Registry:  
`io.github.Anteos-Health/anteos-booking`

---

[Full documentation](https://anteoshealth.com/docs/mcp) · [Anteos Health](https://anteoshealth.com)
