# Recon Skill for Claude Code

Reconnaissance skill for Claude Code agent using **subfinder** and **httpx** for subdomain enumeration and web asset discovery.

### Installation

#### Clone this repository:

```bash
git clone https://github.com/ikajakam/Claude_Skills.git
```

```bash
cp -r claude_skills/recon_skill ~/.claude/skills/
```

### Core Files
- **`recon_SKILL.md`** - Main skill documentation for Claude Code agent
- **`recon_helper.py`** - Python utility for analyzing results and generating reports

### Resource Guides
- **`CONFIG_TEMPLATES.md`** - Configuration templates for subfinder/httpx (API keys, settings)
- **`WORKFLOWS.md`** - 10 pre-built reconnaissance workflows (basic to advanced)
- **`WORDLISTS.md`** - Comprehensive wordlist guide for path discovery

## Usage Prompts

```
"Run reconnaissance on target.com and analyze the results"

"Find all WordPress sites in the scan results"

"Compare the current subdomains with the baseline"

"Show me what technologies are running on these hosts"

"Generate target lists organized by technology"
```

Claude Code will automatically run the appropriate commands and analyze results.

## Features

**Reconnaissance:**
- "Find all subdomains for target.com"
- "Probe the subdomains and detect technologies"
- "Take screenshots of interesting hosts"

**Analysis:**
- "Analyze the results and show me vulnerable versions"
- "What technologies are most common?"
- "Find all admin panels and APIs"

**Organization:**
- "Extract all WordPress sites for testing"
- "Generate organized target lists for fuzzing"
- "Create a report of the findings"

**Monitoring:**
- "Compare this scan with the baseline"
- "Show me new subdomains discovered"
- "Monitor target.com for infrastructure changes"

### Helper Tool Features

For manual use or Claude Code automation:
- **Analyze** - Deep analysis of httpx results (technologies, vulnerabilities, anomalies)
- **Extract** - Filter hosts by technology (WordPress, APIs, etc.)
- **Generate Targets** - Create organized lists for further testing
- **Compare** - Monitor subdomain changes over time
- **Validate** - Check configuration and tool setup
- **Recommend** - Get next-step suggestions based on findings

### Manual Command Reference

<details>
<summary>Click to expand manual commands</summary>

```bash
# Quick summary
python3 recon_helper.py analyze results.json --summary

# Extract WordPress sites
python3 recon_helper.py extract results.json --tech wordpress -o wp-sites.txt

# Generate organized target lists
python3 recon_helper.py generate-targets results.json -o targets/

# Compare old vs new scans
python3 recon_helper.py compare-subs baseline.txt current.txt -o changes.txt

# Get recommendations
python3 recon_helper.py recommend results.json

# Validate setup
python3 recon_helper.py validate-config
```

</details>

## Resource Guides

### CONFIG_TEMPLATES.md
- Subfinder configurations (free & paid API sources)
- Httpx configurations (basic, stealth, aggressive)
- DNS resolvers and custom headers
- Quick setup scripts

### WORKFLOWS.md
Pre-built workflows for:
- Basic subdomain enumeration
- Multi-domain batch processing
- Continuous monitoring
- API-focused reconnaissance
- Large-scale enumeration
- Integration with nuclei, ffuf, naabu

### WORDLISTS.md
Comprehensive guide to:
- Subdomain wordlists (SecLists, Assetnote, etc.)
- Path/directory wordlists for httpx
- Technology-specific lists (WordPress, APIs, admin panels)
- Custom wordlist creation

## Common Workflows

### Comprehensive Recon
```bash
# Complete reconnaissance with analysis
subfinder -d target.com -all -o subdomains.txt
cat subdomains.txt | httpx -silent -tech-detect -json -o results.json
python3 recon_helper.py analyze results.json --report report.html
python3 recon_helper.py generate-targets results.json -o targets/
```

### Continuous Monitoring
```bash
# Initial baseline
subfinder -d target.com -silent > baseline.txt

# Later scan and compare
subfinder -d target.com -silent > current.txt
python3 recon_helper.py compare-subs baseline.txt current.txt -o changes.txt
```

### API Discovery
```bash
subfinder -d target.com -silent | \
  httpx -silent -path /api,/api/v1,/graphql,/swagger.json -mc 200,401,403 -tech-detect
```

### Requirements
- **subfinder** - Subdomain enumeration
- **httpx** - HTTP probing and tech detection

### Optional Tools
- **ffuf** - Content discovery
- **nuclei** - Vulnerability scanning
- **naabu** - Port scanning

### Main skill file (`recon_SKILL.md`) contains:
- Detailed command usage and examples
- Integration patterns
- Best practices for automation
- Error handling guidelines
- Notes specifically for AI agent usage

---

**Note:** This skill is optimized for Claude Code autonomous agent. While the tools and scripts can be used manually, they're designed to work seamlessly with AI-driven workflows.
