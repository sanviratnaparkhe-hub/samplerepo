# Copilot Instructions for AarogyaSaathi

This file guides AI agents on working effectively with this codebase. Update this as the project evolves.

## Project Overview

**Purpose**: AI-powered Digital Health Locker - secure, multi-language healthcare records management system

**Tech Stack**: 
- Single-file HTML5 application with vanilla JavaScript (no build tools required)
- CSS with custom design system (Perplexity-inspired theming)
- Multi-language support (English, Hindi, Tamil, Telugu, Marathi, Bengali)
- GitHub Pages hosting

**Architecture**: Client-side MPA (Multi-Page Application) with role-based dashboards (Patient, Provider, Insurance) and in-memory session management

## Essential Developer Workflows

```bash
# Start local server (test GitHub Pages locally)
python -m http.server 8000
# Then visit: http://localhost:8000/aarogyasathi-health-locker/

# Deploy to GitHub Pages
# Ensure index.html is in aarogyasathi-health-locker/ directory
# GitHub Pages auto-publishes from main branch

# Test multi-language functionality
# Language state stored in _lang global variable (default: 'en')
# Switch via language selector dropdown to verify all LANGDICT entries
```

## Project Conventions & Patterns

- **Single-File Design System**: All CSS uses CSS custom properties (--color-*, --space-*, --font-*); modify :root variables in <style> for theme changes
- **State Management**: Global variables (_user, _lang, _role) simulate session state; no persistence layer (add localStorage if needed)
- **Multi-Language**: Language dictionary (LANGDICT) maps UI strings by language code; add translations to all keys when extending
- **UI Components**: Reusable classes (.btn, .card, .form-control) follow Perplexity design tokens; compose via HTML rather than components
- **Demo Data**: SAMPLE_PATIENTS, SAMPLE_PROVIDERS, SAMPLE_RECORDS provide mock data for testing; replace with API calls in production

## Key Files & Directories

| File | Purpose | Key Pattern |
|---|---|---|
| `aarogyasathi-health-locker/index.html` | Complete app in single file | Splash screen → auth → role-based dashboard flow |

## Integration Points & External Dependencies

- **Fonts**: Loads 'FKGroteskNeue' from `https://r2cdn.perplexity.ai/fonts/FKGroteskNeue.woff2` (fallback: system fonts)
- **No Backend**: Currently simulates API calls with setTimeout; ready for REST/GraphQL integration
- **Authentication**: Mock implementation (demo accounts: SAMPLE_PATIENTS); add OAuth/JWT when needed
- **Storage**: In-memory only; no database (production: add backend DB + API layer)

## Common Pitfalls & Best Practices

- **Do**: Use LANGDICT keys when adding new UI strings; update all 6 languages simultaneously
- **Do**: Test role-based views (patient/provider/insurance) in showDashboard() function to ensure permissions are enforced
- **Do**: Keep inline styles minimal; prefer CSS custom properties from :root for consistency

- **Don't**: Add external frameworks (React, Vue) without refactoring to modular structure
- **Don't**: Store sensitive data in global variables; use sessionStorage or backend sessions
- **Don't**: Break the single-file format without reason—it simplifies GitHub Pages deployment

## Role-Specific Behaviors

- **Patient**: View/upload health records, manage consent grants, track shared data
- **Provider**: Request patient records, view active consents, manage access
- **Insurance**: Track claims, manage consent requests, approve/reject record access

Test all three roles by logging in via SAMPLE_PATIENTS/SAMPLE_PROVIDERS accounts and switching via language selector.

## How to Update This File

1. Document changes with file references (e.g., "line 150 in index.html")
2. Include concrete examples from LANGDICT or showDashboard()
3. When adding features, update this file to explain the new pattern
4. Keep it concise—readers should need only this + code inspection to contribute
