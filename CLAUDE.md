# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**无忧存项目知识库** - A comprehensive documentation repository for 无忧存 (Worry-Free Storage), an O2O luggage storage platform.

**Core Business**: Platform connecting users with luggage storage points across 267 cities in China, with 3353+ merchant locations.

**Major Initiative**: Platform merger project combining 小铁寄存柜 (XiaoTie Smart Lockers) and 无忧存 (Worry-Free Storage) into a unified platform "小铁行李寄存丨无忧存".

## Repository Structure

This is a **documentation repository**, not a codebase. All content is organized as business and technical documentation.

### Primary Directories

```
001-业务全景图 (Business Context)/
├── 品牌介绍/              # Brand introduction
├── 商业计划书（BP）/      # Business plans
├── 年度季度目标/          # OKRs and KPIs
├── 竞品分析/              # Competitor analysis
└── 行业、市场调研报告/    # Market research

002-产品与技术现状 (Product & Tech Stack)/
├── 01-会议纪要/           # Meeting minutes
├── 02-产品架构图/         # Architecture diagrams
│   ├── 信息架构/          # Information architecture
│   ├── 功能架构/          # Functional architecture
│   └── 无忧存业务全景架构列表.md  # **KEY: Complete business architecture**
├── 03-需求、BUG清单/     # Requirements and bugs
├── 04-PRD文档/            # Product requirement documents
│   └── 【小铁无忧存】平台合并项目计划-202510.01.md  # **KEY: Platform merger plan**
├── 05-操作演示手册/       # Operation manuals
└── 06-其他/

003-用户与运营数据 (User & Operations)/
├── FAQ 常见问题集/
├── 历史埋点数据分析/
│   └── 无忧存运营情况报告.md  # **KEY: Operations report**
├── 渠道码/
├── 用户反馈原声/
└── 运营活动复盘/

004-协作流程与制度 (Process & Culture)/
├── 无忧存开发及发布流程.md    # **KEY: Development workflow**
└── 无忧存入口汇总.md          # **KEY: Entry points and routing**

ClaudeCodeSpace/
└── # Working directory for Claude-generated analysis and documents
```

## Key Documents to Read First

When starting work on this project, read these documents in order:

1. **`002-产品与技术现状/02-产品架构图/无忧存业务全景架构列表.md`**
   - Complete business architecture (User端/商家端/管理后台)
   - Core modules and features

2. **`002-产品与技术现状/04-PRD文档/【小铁无忧存】平台合并项目计划-202510.01.md`**
   - Platform merger strategy (小铁 + 无忧存)
   - Milestones and timelines
   - Design principles based on user access patterns

3. **`004-协作流程与制度/无忧存开发及发布流程.md`**
   - Git branch strategy (master/pre-master/test-master/feat-xxx)
   - CI/CD with Jenkins
   - Deployment procedures for 3 platforms

4. **`004-协作流程与制度/无忧存入口汇总.md`**
   - Entry points and routing logic
   - QR code handling
   - Source tracking parameters

## Technical Stack

### User-Facing Applications
- **微信小程序** (WeChat Mini Program)
- **支付宝小程序** (Alipay Mini Program)
- **抖音小程序** (Douyin Mini Program)
- **H5** (Mobile web)
  - Test: `https://test-noproblem-h5.wegui.cn`
  - Prod: `https://h5wyc.nbdevice.com`

### Merchant-Facing
- **微信小程序/公众号** (WeChat Mini Program/Official Account)

### Admin Platform
- **PC Web**
  - Test: `https://noproblem-web.wegui.cn` (admin/123456)
  - Prod: `https://adminnoproblem.nbdevice.com`

### Payment Platforms
- 微信商户平台 (WeChat Pay)
- 汇付 (Huifu)
- 支付宝 (Alipay)

## Development Workflow

### Branch Strategy

| Branch | Purpose |
|--------|---------|
| `master` | Main development branch, create feature branches from here |
| `public` | H5 production deployment branch |
| `pre-master` | Pre-release branch (used as release branch, no pre-prod env) |
| `test-master` | Testing branch |
| `feat-xxx-xxx` | Feature branch (TAPD task ID + name initials) |
| `fix-xxx-xxx` | Bug fix branch (TAPD task ID + name initials) |

### Deployment Process

**User端 (C端)**:
1. Submit merge request to `test-master` → Auto-deploy to test (Jenkins CI/CD)
2. Test and validate
3. Submit merge request to `pre-master` → Auto-deploy to staging
4. Manual submit for review on platform (WeChat/Alipay/Douyin)
5. Version number auto-incremented from git tag

**Merchant端 (B端)**:
- Manual build and upload (low frequency, no automation yet)

**PC Admin**:
- Push to `test-master` → Auto-build + DingTalk notification
- Push to `master` → Auto-build + DingTalk notification to backend for manual deployment

## Platform Merger Context

**Critical Understanding**: The platform is merging two distinct products with different user behaviors:

| Aspect | 小铁寄存柜 | 无忧存 | Merger Challenge |
|--------|----------|-------|-----------------|
| **Access Pattern** | 80%+ offline QR scan | 60% search | Dual-scenario UI required |
| **Usage Scenario** | On-site scan-and-store | Pre-booking online | Different user flows |
| **Age Profile** | Tourism + business | Younger (60% under 30) | UI style balance |
| **Homepage Need** | Direct camera for QR | Search + map | Layout conflict |

**Design Principle**: Intelligent scenario detection
- QR scan entry → Direct camera activation
- Search entry → Highlight search/map features
- First-time users → Guide to choose preference

## Business Model

**Revenue Streams**:
1. Storage service fees (primary)
2. Merchant onboarding deposits
3. Advertising (planned)

**Commission Structure**:
- Merchant: Fixed percentage
- Agent: Tiered (L1/L2)
- Platform: Remainder

## User Journey Pain Points (Based on Latest Analysis)

**P0 Critical Issues**:
1. Anti-crawling strategy hurts conversion (details hidden until booking)
2. Users can't find stores (GPS inaccuracy + limited photos)
3. Homepage function priority confusion (3 modules, unclear hierarchy)
4. Unreasonable cancellation fees (merchant fault still charges user)

**P1 Serious Issues**:
1. Information architecture lacks hierarchy (details page)
2. Redundant entry points (4 paths to same destination)
3. Mandatory coupon usage (no user control)
4. "Feidian" (offline cash transactions) lack prevention

See `ClaudeCodeSpace/无忧存用户旅程地图梳理-20260306.md` for complete analysis.

## Anti-Feidian Strategy

"Feidian" (飞单) = Merchants bypassing platform to collect cash directly, causing 20-30% revenue loss.

**10 Prevention Strategies** (detailed in `ClaudeCodeSpace/防飞单策略整理-20260306.md`):
- Tiered commission (70%→85% based on volume)
- Traffic prioritization algorithm
- Deposit system (¥2000→¥0 for top merchants)
- Insurance binding (platform orders only)
- Points & membership tiers
- QR code verification workflow
- Behavioral tracking
- Cross-platform data comparison

**ROI**: 2-month payback period, 866% ROI

## Working with This Repository

### Adding New Analysis

Place Claude-generated analysis documents in `ClaudeCodeSpace/` with naming convention:
- Format: `{主题}-{YYYYMMDD}.md`
- Example: `无忧存用户旅程地图梳理-20260306.md`

### Document Types

- **会议纪要** (.md files in 01-会议纪要/): Meeting minutes with decisions and action items
- **PRD文档** (.md files in 04-PRD文档/): Product requirement documents with specs and wireframes
- **运营数据** (.md files in 003-用户与运营数据/): Data analysis reports and metrics

### Version Control Principles

For markdown documentation (this repo):
- Append dates to filenames for versioning: `文档名称-YYYYMMDD.md`
- Keep historical versions when major updates occur
- Add update log at top of document

For code repositories (referenced in docs):
- Follow git flow with feature branches
- Never use `git add .` or `git add -A` (specify files to avoid secrets)
- Never skip hooks (`--no-verify`)
- Create NEW commits, avoid `--amend` unless explicitly requested

## Data and Metrics

**Key Metrics** (from operational reports):
- Homepage search usage: 55%+ (name search 35.63% + find button 19.76%)
- "Nearby" module click rate: 4.66% (underperforming, needs redesign)
- WeChat search traffic: 60% of total
- Network coverage: 3353 merchant stores, 267 cities
- Estimated Feidian rate: 20-30%

## Common Tasks

### Understanding Product Architecture
```bash
# Read business architecture overview
cat "002-产品与技术现状 (Product & Tech Stack)/02-产品架构图/无忧存业务全景架构列表.md"
```

### Understanding Platform Merger
```bash
# Read merger plan
cat "002-产品与技术现状 (Product & Tech Stack)/04-PRD文档/【小铁无忧存】平台合并项目计划-202510.01.md"
```

### Accessing Latest Analysis
```bash
# List recent Claude-generated analysis
ls -lt ClaudeCodeSpace/*.md | head -5
```

### Finding Specific Topics
```bash
# Search across all documents
find . -name "*.md" -exec grep -l "关键词" {} \;

# Example: Find all documents about user journey
find . -name "*.md" -exec grep -l "用户路径\|用户旅程" {} \;
```

## Important Notes

1. **This is a documentation repository** - No code compilation or testing required
2. **Platform context is critical** - Always understand 小铁 vs 无忧存 differences when analyzing features
3. **User behavior drives design** - Scan-first (小铁) vs Search-first (无忧存) dictate different UX patterns
4. **Feidian prevention** - Revenue protection is a top priority, any payment flow changes must consider anti-feidian measures
5. **Multi-platform deployment** - Changes affect WeChat, Alipay, Douyin mini-programs simultaneously
6. **CI/CD is automated** - Merging to test/pre-master branches triggers auto-deployment

## Contact Information

**Project Leadership** (from merger plan):
- Product Integration: 周晓洁
- Business Design: 曾文静、石佳惠
- Tech Architecture: 师详
- Project Management: 何荣兴 (13652360712)

## Document Versioning

Latest comprehensive analysis documents in `ClaudeCodeSpace/`:
- `无忧存用户旅程地图梳理-20260306.md` - Complete user journey with pain points
- `防飞单策略整理-20260306.md` - Anti-feidian prevention strategies
- `无忧存用户旅程地图.html` - Interactive visualization of user journey
