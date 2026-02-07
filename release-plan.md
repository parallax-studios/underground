# UNDERGROUND -- Release Plan

**Author**: SHIP (Release Manager)
**Status**: Pre-Production Release Plan
**Version**: 1.0
**Date**: 2026-02-07
**Target Platform**: PC (Steam) Primary, Steam Deck Validated

---

## 1. Executive Summary

This is the document that keeps us from having another launch day disaster. UNDERGROUND is a multi-genre street culture game with four disciplines, emergent AI, and 2000s aesthetic. The complexity is real. The failure points are many. But if we follow this checklist, test on clean machines, and have our rollback plan ready, we'll make launch day boring.

Boring is good. Boring means nothing went wrong.

**Core Release Thesis**: Ship on Steam with full Steamworks integration. Validate on Steam Deck. Have rollback procedures for every critical system. Test the build on clean machines until we're sick of it. Never skip a checklist item.

**Key Dates** (TBD based on development timeline):
- Code Complete (CC): Month 16
- Gold Master (GM): Month 17, Week 3
- Pre-Launch Review Embargo: GM +1 week
- Launch Day: Month 18, Week 1
- First Patch Window: Launch +1 week

---

## 2. Master Launch Checklist

Every item gets a checkbox. Every checkbox gets a date. Every date gets an owner. If it's not on this list, it doesn't happen. If it's on this list and you skip it, we have a conversation.

### 2.1 Build Readiness

**Owner**: BYTE (Lead Programmer) + CRASH (QA Lead)

| ID | Task | Status | Date | Notes |
|----|------|--------|------|-------|
| B-01 | Code complete declared (no new features) | [ ] | CC | Hard stop on feature work |
| B-02 | All critical bugs closed (P0/P1) | [ ] | CC + 1 week | No exceptions |
| B-03 | Gold Master candidate build generated | [ ] | GM - 1 week | First GM candidate |
| B-04 | GM candidate tested on Windows 10 clean machine | [ ] | GM - 5 days | Fresh OS install, no dev tools |
| B-05 | GM candidate tested on Windows 11 clean machine | [ ] | GM - 5 days | Fresh OS install, no dev tools |
| B-06 | GM candidate tested on Steam Deck | [ ] | GM - 5 days | Performance validation 60fps minimum |
| B-07 | GM candidate stress test (4-hour session) | [ ] | GM - 4 days | Check for memory leaks, crashes |
| B-08 | Save/load tested across GM candidate (new save, old save migration if applicable) | [ ] | GM - 4 days | Don't corrupt player saves |
| B-09 | All four disciplines tested to completion in GM | [ ] | GM - 3 days | Racing, Fighting, Basketball, Tricks |
| B-10 | Steam Cloud save sync tested (upload/download) | [ ] | GM - 3 days | Test on two machines |
| B-11 | Controller input tested (Xbox, PS5, generic) | [ ] | GM - 3 days | All button mappings work |
| B-12 | Keyboard/mouse tested (secondary input) | [ ] | GM - 2 days | All controls functional |
| B-13 | Build version number finalized (1.0.0) | [ ] | GM - 1 day | Update in code + Steam config |
| B-14 | Final GM build approved by BYTE + CRASH | [ ] | GM | Go/No-Go decision |
| B-15 | GM build uploaded to Steam (private branch) | [ ] | GM | Master build secured |

### 2.2 Platform Configuration (Steamworks)

**Owner**: SHIP (Release Manager)

| ID | Task | Status | Date | Notes |
|----|------|--------|------|-------|
| P-01 | Steam App ID created (via Steamworks backend) | [ ] | Month 12 | Early to allow testing |
| P-02 | Steam Depot configured (Windows x64) | [ ] | Month 12 | Primary platform |
| P-03 | Steam Depot configured (Linux x64 for Deck) | [ ] | Month 12 | Secondary platform |
| P-04 | Steamworks SDK integrated into build | [ ] | Month 13 | Steamworks.NET |
| P-05 | Steam Achievements configured (25 achievements) | [ ] | GM - 2 weeks | Achievement list from design doc |
| P-06 | Steam Achievements tested in dev build | [ ] | GM - 1 week | Trigger all 25, verify unlock |
| P-07 | Steam Cloud enabled and quota set (50MB max) | [ ] | GM - 1 week | Save files are small, 50MB plenty |
| P-08 | Steam Controller API configured (Steam Input) | [ ] | GM - 1 week | Allows rebinding in Steam overlay |
| P-09 | Steam Trading Cards designed (if applicable) | [ ] | GM - 1 week | Optional, 30-day post-launch |
| P-10 | Steam Store page text finalized | [ ] | GM - 2 weeks | Copywriting complete |
| P-11 | Steam Store capsule art uploaded (all sizes) | [ ] | GM - 2 weeks | 460x215, 231x87, 184x69, etc. |
| P-12 | Steam Store screenshots uploaded (10 minimum) | [ ] | GM - 2 weeks | All four disciplines shown |
| P-13 | Steam Store trailer uploaded (1-2 min) | [ ] | GM - 2 weeks | Hook in first 10 seconds |
| P-14 | Steam Store page "Coming Soon" published | [ ] | GM - 4 weeks | Build wishlist pre-launch |
| P-15 | Steam Regional Pricing configured (all regions) | [ ] | GM - 1 week | Use Steam's auto-pricing or custom |
| P-16 | Steam Launch Discount configured (10% launch week) | [ ] | GM - 3 days | Optional, discuss with HYPE |
| P-17 | Steam Pre-Purchase enabled (if applicable) | [ ] | GM - 2 weeks | Only if confident in launch date |
| P-18 | Steam Review Keys generated (50 keys for press) | [ ] | Launch - 2 weeks | Distribution via Terminals, Keymailer |
| P-19 | Steam Community Hub moderation plan | [ ] | Launch - 1 week | Who monitors forums/discussions |
| P-20 | Steam Build uploaded to default branch (launch) | [ ] | Launch Day, 10am PST | The big button |

### 2.3 Age Rating & Compliance

**Owner**: SHIP (Release Manager) + Legal (if applicable)

| ID | Task | Status | Date | Notes |
|----|------|--------|------|-------|
| C-01 | IARC age rating questionnaire submitted | [ ] | GM - 4 weeks | International Age Rating Coalition (easiest path) |
| C-02 | ESRB rating received (expected: Teen for fantasy violence, mild language) | [ ] | GM - 2 weeks | US rating |
| C-03 | PEGI rating received (expected: 12 or 16) | [ ] | GM - 2 weeks | EU rating |
| C-04 | Age rating icons added to store page | [ ] | GM - 1 week | Required by Steam |
| C-05 | Content warning labels added (if applicable) | [ ] | GM - 1 week | Violence, language, in-game purchases |
| C-06 | EULA finalized | [ ] | GM - 2 weeks | Standard Steam EULA or custom |
| C-07 | Privacy Policy finalized (if collecting data) | [ ] | GM - 2 weeks | GDPR compliance |
| C-08 | Third-party licenses documented (credits screen) | [ ] | GM - 1 week | Unity, middleware, fonts, etc. |
| C-09 | Music licensing confirmed (original OST or licensed) | [ ] | GM - 4 weeks | No unlicensed tracks |
| C-10 | No trademarked IP violations (car brands, etc.) | [ ] | GM - 4 weeks | All cars are fictional or licensed |

### 2.4 Marketing & Community

**Owner**: HYPE (Marketing) + SHIP (Release Manager)

| ID | Task | Status | Date | Notes |
|----|------|--------|------|-------|
| M-01 | Launch trailer finalized (1-2 min) | [ ] | Launch - 3 weeks | Shows all four disciplines |
| M-02 | Launch trailer uploaded to YouTube | [ ] | Launch - 2 weeks | Public or unlisted until launch |
| M-03 | Press kit prepared (screenshots, key art, fact sheet) | [ ] | Launch - 3 weeks | Hosted on presskit() site |
| M-04 | Review embargo date set (Launch - 1 week) | [ ] | Launch - 4 weeks | Coordinate with press |
| M-05 | Review keys distributed (50 keys to press/influencers) | [ ] | Launch - 2 weeks | Track who got keys |
| M-06 | Social media accounts active (Twitter, Discord, Reddit) | [ ] | Launch - 4 weeks | Post devlog updates |
| M-07 | Discord server set up (community hub) | [ ] | Launch - 4 weeks | Moderation plan in place |
| M-08 | Launch day social media plan (tweet schedule) | [ ] | Launch - 1 week | Every 2 hours on launch day |
| M-09 | Launch day announcement blog post (Steam + website) | [ ] | Launch - 3 days | Goes live at launch |
| M-10 | Influencer outreach complete (streamers, YouTubers) | [ ] | Launch - 2 weeks | Keys sent, embargo explained |
| M-11 | Press outreach complete (Polygon, IGN, PC Gamer, etc.) | [ ] | Launch - 2 weeks | Keys sent, embargo explained |
| M-12 | Launch day Discord event (dev AMA or similar) | [ ] | Launch Day | Community engagement |

### 2.5 Post-Launch Monitoring

**Owner**: SHIP (Release Manager) + CRASH (QA Lead)

| ID | Task | Status | Date | Notes |
|----|------|--------|------|-------|
| L-01 | Launch day war room (Discord channel, all hands) | [ ] | Launch Day | Monitor for 8 hours minimum |
| L-02 | Steam forums monitored (check every 30 min) | [ ] | Launch Day | First 48 hours critical |
| L-03 | Discord monitored (check every 30 min) | [ ] | Launch Day | Community will report bugs fast |
| L-04 | Twitter mentions monitored | [ ] | Launch Day | Social listening |
| L-05 | Crash reporting enabled (Unity Analytics or Sentry) | [ ] | Launch Day | Backend crash logs |
| L-06 | Performance metrics tracked (FPS, load times) | [ ] | Launch Day | Unity Analytics or custom |
| L-07 | Critical bug triage protocol active | [ ] | Launch Day | P0 bugs get hotfix immediately |
| L-08 | Hotfix build pipeline ready (emergency patch) | [ ] | Launch Day | Can ship patch in <24 hours |
| L-09 | Day 1 patch prepared (known non-critical bugs) | [ ] | Launch + 1 day | Optional, only if needed |
| L-10 | Week 1 patch prepared (balance, QOL fixes) | [ ] | Launch + 1 week | Expected post-launch polish |

---

## 3. Build Pipeline Documentation

This is how we go from "code on a developer's machine" to "shippable gold master." Every step is documented. Every step is repeatable. If the lead programmer gets hit by a bus, someone else can cut the GM build from this doc.

### 3.1 Build Environment Setup

**Machine Requirements**:
- OS: Windows 10/11 x64 (clean install, no dev tools except what's listed)
- Unity 2022.3 LTS (exact version locked in project)
- Git LFS configured
- Unity build tools installed
- Steam SDK installed (for Steamworks integration)

**Source Control**:
- Repo: GitHub (private repo until launch)
- Branch: `main` (always shippable)
- Tag convention: `v1.0.0-GM` for Gold Master

**Build Machine** (dedicated, not dev machine):
- Cloud build server (Unity Cloud Build or GitHub Actions runner)
- Automated builds on commit to `main`
- Manual builds on demand for GM candidates

### 3.2 Build Process (Step-by-Step)

**Pre-Build Checks**:
1. Verify `main` branch is stable (all CI tests pass)
2. Verify no pending critical bugs (P0/P1)
3. Verify build version number is updated in `ProjectSettings/ProjectSettings.asset` and `GameVersion.cs`
4. Verify all scenes are added to Build Settings
5. Verify all Addressables are built and validated

**Build Steps** (Windows x64):
1. Open Unity 2022.3 LTS
2. Load project from repo (clean clone, not dev workspace)
3. Switch to Windows x64 build target (File > Build Settings)
4. Set build configuration to "Release" (not "Development Build")
5. Disable "Script Debugging" and "Deep Profiling"
6. Enable "Compression Method: LZ4" (faster load times)
7. Build Addressables: Window > Asset Management > Addressables > Build > New Build > Default Build Script
8. Build Player: File > Build Settings > Build
9. Output directory: `Builds/Windows/UNDERGROUND_v1.0.0/`

**Post-Build Validation**:
1. Check build size (target: <5GB for Windows build)
2. Launch build on build machine (smoke test: main menu loads, start new game, first district loads)
3. Check build logs for errors/warnings (ignore harmless shader warnings)
4. Zip build folder: `UNDERGROUND_v1.0.0_Windows.zip`
5. Generate SHA256 checksum (for verification)

**Linux x64 Build** (for Steam Deck):
1. Same steps as Windows, but switch to Linux x64 target
2. Test on Steam Deck hardware (if available) or SteamOS VM
3. Proton compatibility verified (Unity 2022.3 LTS is Proton-compatible)

**Build Artifacts**:
- `UNDERGROUND_v1.0.0_Windows.zip` (primary)
- `UNDERGROUND_v1.0.0_Linux.zip` (secondary)
- `BuildLog_v1.0.0.txt` (Unity build log)
- `SHA256_v1.0.0.txt` (checksum file)

**Storage**:
- Upload to AWS S3 or Google Drive (team-accessible)
- Upload to Steam (via Steamworks SDK, `steamcmd` tool)

### 3.3 Steam Upload Process

**Tools**: SteamCMD (command-line tool for uploading builds to Steam)

**Setup**:
1. Install SteamCMD: https://developer.valvesoftware.com/wiki/SteamCMD
2. Configure app build script (VDF file):

```vdf
"AppBuild"
{
    "AppID" "YOUR_APP_ID"
    "Desc" "UNDERGROUND v1.0.0 GM"
    "BuildOutput" "C:\SteamBuilds\Output\"
    "ContentRoot" "C:\Builds\UNDERGROUND_v1.0.0\"
    "SetLive" "default"

    "Depots"
    {
        "DEPOT_ID_WINDOWS"
        {
            "FileMapping"
            {
                "LocalPath" "*"
                "DepotPath" "."
            }
        }
        "DEPOT_ID_LINUX"
        {
            "FileMapping"
            {
                "LocalPath" "*"
                "DepotPath" "."
            }
        }
    }
}
```

**Upload Steps**:
1. Run SteamCMD: `steamcmd.exe`
2. Login: `login YOUR_STEAM_USERNAME`
3. Upload build: `run_app_build C:\path\to\app_build.vdf`
4. Wait for upload (5-30 minutes depending on build size and connection)
5. Verify on Steamworks backend (build appears in "Builds" tab)
6. Set build live on branch (e.g., "default" for public, "beta" for testing)

**Post-Upload Validation**:
1. Download build from Steam (on clean machine, not dev machine)
2. Launch via Steam client
3. Verify Steam overlay works (Shift+Tab)
4. Verify achievements unlock (test one achievement)
5. Verify cloud saves sync (save on machine A, load on machine B)

### 3.4 Version Control & Tagging

**Git Tagging** (for GM):
```bash
git tag -a v1.0.0-GM -m "Gold Master build for launch"
git push origin v1.0.0-GM
```

**Branch Protection**:
- `main` branch is protected (no force pushes)
- GM tag is immutable (cannot delete or overwrite)
- If GM has critical bug, create new tag `v1.0.1-GM` (do NOT overwrite v1.0.0-GM)

**Build Reproducibility**:
- Lock Unity version (2022.3.X, specific patch version)
- Lock all package versions (no auto-update)
- Document all third-party DLLs and versions
- If we need to rebuild GM six months later, we can checkout the tag and rebuild identically

---

## 4. Platform Configuration Checklist (Steamworks)

Steam is not just a download platform. It's achievements, cloud saves, controller support, community features, regional pricing, and a hundred other things. Each one is a potential launch day failure point. We configure everything, test everything, document everything.

### 4.1 Steamworks App Setup

**App ID**: (TBD, assigned by Steam after partner approval)

**App Name**: UNDERGROUND

**App Type**: Game

**Release State**: Coming Soon (pre-launch) -> Released (launch day)

**Platform Support**:
- Windows (primary)
- Linux (Steam Deck validated)
- macOS (not supported at launch)

### 4.2 Steam Achievements Configuration

**Total Achievements**: 25

**Achievement Breakdown** (examples, final list from design):
- **First Night Out**: Complete your first event (any discipline)
- **Drift King**: S-Rank a racing event
- **Knockout Artist**: S-Rank a fighting event
- **Ankle Breaker**: S-Rank a basketball event
- **Combo Master**: S-Rank a tricks event
- **Known in the Streets**: Reach LOCAL REP tier (1,000 REP)
- **Legendary Status**: Reach LEGENDARY REP tier (35,000 REP)
- **Crew Up**: Recruit your first rival
- **Obsession**: Have a rival enter Obsessed state
- **Breaking Point**: Break a rival (confidence hits 0)
- **Four Disciplines**: Complete one event in each discipline
- **Cross-Training**: Complete a cross-discipline style chain (Race->Fight->Ball)
- **Synergy Seeker**: Unlock a build synergy
- **Southside Boss**: Defeat the Southside district boss
- **Docks Boss**: Defeat the Docks district boss
- **Midtown Boss**: Defeat the Midtown district boss
- **Heights Boss**: Defeat the Heights district boss
- **Underground King**: Choose the underground path (story choice)
- **Mainstream Icon**: Choose the mainstream path (story choice)
- **Best of Both**: Complete both paths (hidden achievement)
- **Fully Loaded**: Own 10 cars
- **Fashion Forward**: Own 20 clothing items
- **Master Technician**: Reach proficiency 10 in any discipline
- **Jack of All Trades**: Reach proficiency 5 in all four disciplines
- **S-Rank Legend**: S-Rank 50 events

**Implementation**:
- Achievements triggered via Steamworks API: `SteamUserStats.SetAchievement("ACHIEVEMENT_ID")`
- Test achievements in dev build (Steam's "Reset Stats/Achievements" for testing)
- Achievements unlock retroactively (if player meets conditions, achievement unlocks even if game didn't track it properly - use save data to check on load)

**Achievement Icons**:
- 64x64 PNG (locked and unlocked states)
- Designed by PIXEL (Art Director)
- Uploaded to Steamworks backend

### 4.3 Steam Cloud Saves

**Quota**: 50MB (more than enough for JSON save files)

**Files to Sync**:
- `save.json` (player save data, ~500KB)
- `settings.json` (player settings, ~10KB)
- `achievements.dat` (local achievement cache for offline play, ~5KB)

**Implementation**:
- Use Steam's `ISteamRemoteStorage` API
- On save: `SteamRemoteStorage.FileWrite("save.json", data)`
- On load: Check Steam Cloud for newer save, download if exists

**Conflict Resolution**:
- Steam shows "newer save on cloud vs. local" dialog to player
- Player chooses which to keep
- We don't auto-resolve (player decides)

**Testing**:
- Save on machine A, launch on machine B (cloud save downloads)
- Play on machine B, save, launch on machine A (cloud save updates)
- Test offline mode (save locally, sync when back online)

### 4.4 Steam Input (Controller Support)

**Controller API**: Steam Input (allows rebinding via Steam overlay)

**Supported Controllers**:
- Xbox One/Series controller (primary)
- PS4/PS5 DualShock/DualSense (secondary)
- Steam Deck built-in controls (validated target)
- Generic controllers (if they map to standard gamepad layout)

**Input Binding**:
- Use Unity's Input System package
- Configure Steam Input layout (via Steamworks backend)
- Allow players to rebind in Steam overlay (Big Picture mode)

**Testing**:
- Test all four disciplines with Xbox controller
- Test all four disciplines with PS5 controller
- Test on Steam Deck (built-in controls)
- Test keyboard/mouse as fallback

### 4.5 Steam Store Page Configuration

**Store Page Sections**:
1. **Capsule Art** (all sizes):
   - Header: 460x215
   - Small capsule: 231x87
   - Main capsule: 616x353
   - Library capsule: 600x900
2. **Screenshots** (minimum 10):
   - All four disciplines shown
   - 1920x1080 resolution
   - Show UI, show gameplay, show style meter, show rivals
3. **Trailer** (1-2 minutes):
   - Hook in first 10 seconds (the cross-discipline GIF moment)
   - Show all four disciplines
   - Show style meter, REP system, rival system
   - Show 2000s aesthetic (CRT filter, underglow, etc.)
   - End with logo + release date
4. **Description** (written by HYPE):
   - Short description (1-2 sentences, appears in search)
   - Long description (5-10 paragraphs, full pitch)
   - Feature list (bullets)
5. **System Requirements**:
   - Minimum: Intel i5-6600, GTX 960, 8GB RAM, 10GB storage, Windows 10
   - Recommended: Intel i5-9600, RTX 2060, 16GB RAM, 10GB storage, Windows 11
   - Steam Deck: Validated (60fps at 800p)
6. **Tags** (Steam's discovery system):
   - Racing, Fighting, Sports, Action, Indie, Singleplayer, Controller, Arcade, 2000s, Street Culture, Character Customization, Choices Matter, Atmospheric, Stylized
7. **Languages**:
   - English (full audio + text)
   - (Optional: French, German, Spanish text localization post-launch)

**Store Page Launch Timeline**:
- GM - 4 weeks: "Coming Soon" page goes live (builds wishlist)
- Launch Day, 10am PST: Store page goes live with "Buy Now" button

### 4.6 Regional Pricing

**Base Price**: $19.99 USD (discuss with HYPE, this is suggested pricing)

**Regional Pricing** (use Steam's auto-conversion or manual):
- USD: $19.99
- EUR: €18.99
- GBP: £16.99
- JPY: ¥2,200
- CNY: ¥68
- (etc. for all Steam-supported regions)

**Launch Discount**: 10% off for first week (discuss with HYPE)
- Launch price: $17.99 USD
- Returns to $19.99 after 1 week

**Key Considerations**:
- Steam takes 30% cut (revenue = 70% of sale price)
- Regional pricing affects discoverability (Steam's algorithm favors fair pricing)
- Adjust for purchasing power parity (don't charge Argentina same as US)

### 4.7 Steam Community Features

**Community Hub**:
- Forums (Steam provides)
- Discussions (Steam provides)
- Workshop (not planned for launch, potential post-launch for custom districts)
- Screenshots (Steam provides)
- Artwork (Steam provides)

**Moderation Plan**:
- Assign 1-2 team members to monitor forums daily (first 2 weeks post-launch)
- Respond to bug reports within 24 hours
- Community guidelines posted (no toxicity, spoiler tags required, etc.)

**Trading Cards** (optional, post-launch):
- Designed 30 days after launch (Steam requirement)
- 5-10 cards (collectible, cosmetic)
- Badges, emoticons, profile backgrounds (player rewards for engagement)

---

## 5. Rollback and Hotfix Procedures

Launch day goes wrong. Always. The question is: how fast can we fix it? If we have a P0 bug (game-breaking, crashes, saves corrupted), we need a hotfix live within 24 hours. If we can't fix it in 24 hours, we roll back to the previous build.

This section is the emergency manual. If you're reading this on launch day because something is on fire, follow these steps exactly.

### 5.1 Rollback Procedure (Emergency Build Revert)

**When to Roll Back**:
- Game won't launch for >50% of players
- Save data corruption (widespread reports)
- Critical exploit (infinite money, etc.)
- Performance regression (game unplayable, <30fps on target hardware)

**Rollback Steps**:
1. **Assess severity** (war room decision, 5-minute discussion)
   - Is this a P0 bug? (game-breaking, affects majority of players)
   - Can we hotfix in <24 hours? (if yes, hotfix instead of rollback)
   - If no, proceed with rollback
2. **Identify previous stable build**:
   - Last known good build (e.g., v1.0.0-GM if current is v1.0.1)
   - Verify previous build is on Steam (in "Builds" tab on Steamworks backend)
3. **Set previous build live**:
   - Log into Steamworks backend
   - Navigate to "Builds" tab
   - Select previous build (e.g., v1.0.0-GM)
   - Set live on "default" branch (this pushes to all players)
   - Estimated time to rollback: 5 minutes
4. **Communicate to players**:
   - Post on Steam forums: "We've identified a critical issue and have rolled back to the previous build. We're working on a fix. ETA: [X hours]."
   - Post on Discord, Twitter (same message)
   - Pin message in Steam forums
5. **Work on hotfix**:
   - Fix the bug in `main` branch
   - Cut new build (v1.0.2)
   - Test on clean machine
   - Upload to Steam (private beta branch first, test internally)
   - If stable, set live on "default" branch
   - Communicate to players: "Issue resolved, new build live."

**Rollback SLA** (Service Level Agreement):
- Decision to roll back: <30 minutes from bug discovery
- Rollback executed: <5 minutes from decision
- Total time from bug discovery to rollback live: <35 minutes

### 5.2 Hotfix Procedure (Emergency Patch)

**When to Hotfix**:
- P0 bug discovered post-launch (game-breaking but not widespread enough to rollback)
- Exploit discovered (needs immediate patch)
- Critical performance issue (fixable with targeted optimization)

**Hotfix Steps**:
1. **Identify the bug**:
   - Reproduce on dev machine
   - Identify root cause (code review, profiling, logs)
   - Estimate fix time (if >24 hours, consider rollback instead)
2. **Fix the bug**:
   - Create hotfix branch from GM tag: `git checkout -b hotfix/v1.0.1 v1.0.0-GM`
   - Apply minimal fix (change as little code as possible)
   - Test fix on dev machine
   - Commit fix: `git commit -m "[HOTFIX] Fix save corruption bug"`
3. **Cut hotfix build**:
   - Build from hotfix branch
   - Version number: v1.0.1 (increment patch version)
   - Test on clean machine (full smoke test: launch, load save, play 10 minutes)
   - If stable, proceed
4. **Upload to Steam (beta branch first)**:
   - Upload to "beta" branch on Steam (not "default")
   - Test internally (team downloads beta build, tests for 1-2 hours)
   - If stable, set live on "default" branch
5. **Merge hotfix to main**:
   - `git checkout main`
   - `git merge hotfix/v1.0.1`
   - `git push origin main`
   - Tag hotfix: `git tag v1.0.1` and `git push origin v1.0.1`
6. **Communicate to players**:
   - Post on Steam forums: "Hotfix v1.0.1 live, addresses [bug description]."
   - Post on Discord, Twitter
   - Steam auto-updates players (no action required from them)

**Hotfix SLA**:
- Decision to hotfix: <1 hour from bug discovery
- Fix developed: <12 hours from decision
- Build tested and uploaded: <4 hours from fix complete
- Total time from bug discovery to hotfix live: <18 hours

### 5.3 Known Issues & Day-One Patch

Some bugs are known at GM but not critical enough to delay launch. We document them, ship anyway, and patch within the first week.

**Day-One Patch Candidate List** (TBD based on final QA):
- Non-critical bugs (UI glitches, minor balance issues, typos)
- Performance optimizations (if Steam Deck is 55fps instead of 60fps, patch to hit 60fps)
- Quality-of-life improvements (based on early player feedback)

**Day-One Patch Timeline**:
- GM: Known issues documented
- Launch Day: Monitor for additional issues
- Launch + 1 day: Triage all reported issues (P0, P1, P2)
- Launch + 3 days: Day-one patch build ready
- Launch + 4 days: Day-one patch tested
- Launch + 5-7 days: Day-one patch live

**Communication**:
- Known issues posted on Steam forums at launch (transparency)
- "We're aware of [X], patch coming [date]"
- Players appreciate honesty more than silence

---

## 6. Launch Day Timeline (Hour-by-Hour)

Launch day is choreographed. Every hour, we have tasks. Every task, we have an owner. This is the script.

**Launch Date**: TBD (Month 18, Week 1)
**Launch Time**: 10:00 AM PST (Steam standard launch time)

### 6.1 Pre-Launch (Launch - 7 Days)

**Launch - 7 Days** (Monday):
- [ ] Final GM build uploaded to Steam (private branch)
- [ ] Review embargo lifts (press can publish reviews)
- [ ] Monitor review scores (target: 75+ on Metacritic/OpenCritic)
- [ ] Prepare launch day social posts (queue 10 tweets, Discord announcements)

**Launch - 3 Days** (Friday):
- [ ] Final store page check (typos, screenshots, trailer)
- [ ] Final build test on clean machines (Windows, Linux)
- [ ] Confirm launch time with Steam (10am PST)
- [ ] War room Discord channel created (all hands on deck)

**Launch - 1 Day** (Sunday):
- [ ] Final go/no-go meeting (SHIP + BYTE + CRASH + HYPE + CLOCK)
- [ ] If go: confirm launch
- [ ] If no-go: delay launch, communicate to press/community
- [ ] Prep launch day snacks (war room will be long)

### 6.2 Launch Day (Hour-by-Hour)

All times in PST.

**08:00 AM - Pre-Launch Briefing**:
- [ ] War room opens (Discord voice channel)
- [ ] All team members check in
- [ ] Review launch checklist (this document)
- [ ] Assign monitoring roles:
  - SHIP: Steamworks backend, build status
  - CRASH: Steam forums, bug reports
  - HYPE: Social media, press outreach
  - BYTE: Crash logs, backend monitoring
  - CLOCK: Timeline management, decision-making

**09:00 AM - Final Checks**:
- [ ] SHIP: Verify GM build is on "default" branch (not live yet)
- [ ] SHIP: Verify store page is ready (will go live at 10am)
- [ ] HYPE: Queue first social post (goes live at 10am)
- [ ] CRASH: Open Steam forums monitoring (refresh every 5 min)

**10:00 AM - LAUNCH (THE BIG BUTTON)**:
- [ ] SHIP: Set build live on Steam (click "Set Live" on "default" branch)
- [ ] SHIP: Verify store page is live (refresh Steam, check "Buy Now" button)
- [ ] HYPE: Post launch announcement (Twitter, Discord, Reddit, Steam forums)
- [ ] Team: Celebrate (30 seconds, then back to monitoring)

**10:05 AM - First Wave Monitoring**:
- [ ] CRASH: Check Steam forums (any launch issues?)
- [ ] CRASH: Check Discord (community reports)
- [ ] BYTE: Check crash logs (any spikes in crashes?)
- [ ] SHIP: Check Steamworks backend (download stats, concurrent players)

**10:30 AM - 30-Minute Check-In**:
- [ ] War room sync: Any issues?
- [ ] CRASH: Summarize first 30 minutes (# of bug reports, severity)
- [ ] BYTE: Any P0 bugs? (if yes, activate hotfix procedure)
- [ ] SHIP: Download stats (how many players?)

**11:00 AM - 1-Hour Check-In**:
- [ ] Same as 30-minute check-in
- [ ] HYPE: Post 1-hour update on social ("Launch is live, thanks for playing!")

**12:00 PM - 2-Hour Check-In**:
- [ ] Same as above
- [ ] Team: Lunch break (rotate, always have someone monitoring)

**02:00 PM - 4-Hour Check-In**:
- [ ] CRASH: Triage all reported bugs (P0, P1, P2)
- [ ] BYTE: Any patterns in crash logs? (common crash = priority fix)
- [ ] SHIP: Performance metrics (Steam Deck players reporting FPS issues?)

**04:00 PM - 6-Hour Check-In**:
- [ ] War room sync: Go/no-go for hotfix?
- [ ] If hotfix needed: BYTE starts fix, target upload by midnight
- [ ] If no hotfix needed: continue monitoring

**06:00 PM - 8-Hour Check-In**:
- [ ] HYPE: Post end-of-day update on social ("Thanks for the amazing launch day!")
- [ ] CRASH: Final triage (prioritize P0 bugs for tomorrow)
- [ ] Team: Rotate to night shift (if applicable) or end war room

**10:00 PM - 12-Hour Check-In** (optional, if issues):
- [ ] SHIP: Final check before sleep (any fires?)
- [ ] If quiet: team stands down for the night
- [ ] If not quiet: night shift continues monitoring

### 6.3 Post-Launch (Days 1-7)

**Launch + 1 Day** (Tuesday):
- [ ] Morning triage: Review all bugs from Day 1
- [ ] CRASH: Categorize bugs (P0, P1, P2)
- [ ] BYTE: Start work on Day 1 patch (target: Launch + 5-7 days)
- [ ] HYPE: Post-launch community engagement (respond to forums, Discord)

**Launch + 2 Days** (Wednesday):
- [ ] Continue monitoring (Steam forums, Discord, social)
- [ ] BYTE: Day 1 patch development continues
- [ ] SHIP: Check review scores (Metacritic, OpenCritic, Steam reviews)

**Launch + 3 Days** (Thursday):
- [ ] BYTE: Day 1 patch build ready
- [ ] CRASH: Test Day 1 patch on clean machine
- [ ] SHIP: Upload Day 1 patch to beta branch (internal testing)

**Launch + 4 Days** (Friday):
- [ ] Team tests Day 1 patch (all hands, 2-hour playtest)
- [ ] If stable: prepare to set live
- [ ] If not stable: continue fixing

**Launch + 5-7 Days** (Weekend/Monday):
- [ ] SHIP: Set Day 1 patch live on Steam
- [ ] HYPE: Post patch notes (Steam forums, Discord, Twitter)
- [ ] CRASH: Monitor for patch-related issues

**Launch + 7 Days** (End of Week 1):
- [ ] Post-launch retrospective meeting (what went well, what didn't)
- [ ] SHIP: Document lessons learned (add to this doc for future launches)
- [ ] Team: Transition to post-launch support mode (regular cadence, not war room)

---

## 7. Post-Launch Monitoring Plan

Launch week is just the beginning. We monitor for weeks. We patch for months. We support for years (if the game succeeds).

### 7.1 What to Monitor

**Metrics** (via Steam Analytics, Unity Analytics, or custom backend):
- Concurrent players (CCU): How many playing right now?
- Daily active users (DAU): How many unique players per day?
- Session length: Average playtime per session (target: 60-90 min)
- Retention: Day 1, Day 7, Day 30 retention rates
- Completion rate: What % of players reach credits?
- Discipline usage: Are all four disciplines played equally? (if one is ignored, balance issue)
- REP distribution: Where do players plateau? (if everyone stalls at 10k REP, progression issue)
- Crash rate: Crashes per session (target: <1%)
- Performance: Average FPS on Steam Deck (target: 60fps minimum)

**Qualitative Feedback** (via forums, Discord, social):
- Bug reports (categorize by severity)
- Feature requests (what do players want?)
- Balance complaints (what feels unfair?)
- Confusion points (what's not clear?)

### 7.2 Response Cadence

**P0 Bugs** (game-breaking, crashes, save corruption):
- Response time: <1 hour
- Fix time: <24 hours (hotfix procedure)
- Communication: Immediate (post on forums, Discord)

**P1 Bugs** (major issues, not game-breaking):
- Response time: <24 hours
- Fix time: <1 week (Day 1 patch or Week 1 patch)
- Communication: Daily updates on progress

**P2 Bugs** (minor issues, QOL):
- Response time: <1 week
- Fix time: <1 month (monthly patch)
- Communication: Acknowledge in patch notes

**Feature Requests**:
- Response time: <1 week
- Implementation: Post-launch (DLC or free update if game succeeds)
- Communication: "We hear you, considering for future update"

### 7.3 Patching Cadence

**Week 1 Patch**: Bug fixes, performance optimizations (expected)
**Week 4 Patch**: Balance tuning, QOL improvements (based on feedback)
**Month 3 Patch**: Content additions (if game succeeds - new rivals, events)
**Month 6+ Patch**: Major updates or DLC (if game succeeds)

**Patch Testing**:
- Every patch tested on clean machine
- Every patch uploaded to beta branch first (internal testing)
- Every patch announced on forums/Discord before going live

---

## 8. Age Rating and Compliance Notes

UNDERGROUND involves street racing, street fighting, and competitive sports. We're not making a kids' game. But we're also not making an M-rated game. We aim for Teen (ESRB) or 12/16 (PEGI).

### 8.1 IARC Age Rating Questionnaire

**What is IARC?**: International Age Rating Coalition - streamlined age rating process for digital games. One questionnaire gets you ratings for ESRB (US), PEGI (EU), and others.

**How to Apply**:
1. Go to IARC portal: https://www.globalratings.com/
2. Fill out questionnaire (20 minutes)
3. Questions cover: violence, language, drugs, gambling, etc.
4. Submit questionnaire
5. Receive age ratings within 24 hours

**Expected Ratings**:
- ESRB: Teen (13+) - Fantasy violence, mild language, competitive gameplay
- PEGI: 12 or 16 - Violence (non-realistic), bad language (mild)
- USK (Germany): 12
- ACB (Australia): M (15+)

**Content Descriptors** (expected):
- Violence: Street fighting (not realistic, stylized), racing crashes (no blood, no gore)
- Language: Mild language (no F-bombs, some "damn" or "hell" in dialogue)
- Gambling: None (no loot boxes, no real-money gambling)
- In-Game Purchases: None at launch (potential DLC post-launch, but no microtransactions)

### 8.2 Content Warnings

**What Players Should Know**:
- Competitive gameplay (online interactions not rated - but we're single-player at launch, so N/A)
- Stylized violence (fighting, crashes)
- Mild language
- 2000s street culture themes (not illegal activities depicted, but underground culture)

**Store Page Warnings** (if applicable):
- None required for Teen rating
- If we add multiplayer post-launch, add "Online Interactions Not Rated by ESRB"

### 8.3 Music Licensing

**Original Soundtrack**: Composed in-house or contracted (no licensing issues)

**Licensed Music** (if any):
- Clear all rights before launch (sync license, mechanical license)
- Budget for licensing: $5k-$50k per track (depending on artist)
- If budget doesn't allow licensed music: use original OST only
- Do NOT ship with unlicensed tracks (lawsuit risk)

**Alternatives**:
- Use royalty-free music libraries (Artlist, Epidemic Sound)
- Commission original tracks from indie artists (cheaper, unique)
- Sample/remix culture (clear samples or use royalty-free samples)

### 8.4 Third-Party Licenses

**Credits Screen** must include:
- Unity Engine (required by Unity license)
- Steamworks.NET (MIT license, credit appreciated)
- Any other middleware (DOTween, Cinemachine, etc.)
- Font licenses (if using commercial fonts)
- Sound effects libraries (if using commercial SFX packs)

**Sample Credits Screen**:
```
UNDERGROUND
Developed by [Studio Name]

Engine: Unity 2022.3 LTS
Steamworks Integration: Steamworks.NET
UI Animation: DOTween
Camera System: Cinemachine

Fonts: [Font Name] by [Designer]
SFX: [SFX Library] by [Provider]

Special Thanks: [List contributors, playtesters, etc.]
```

---

## 9. Emergency Contacts

If something goes catastrophically wrong on launch day, who do we call?

**Internal Team**:
- SHIP (Release Manager): [Phone/Discord]
- BYTE (Lead Programmer): [Phone/Discord]
- CRASH (QA Lead): [Phone/Discord]
- HYPE (Marketing): [Phone/Discord]
- CLOCK (Producer): [Phone/Discord]

**External Contacts**:
- Steam Support: https://partner.steamgames.com/support (for critical Steam issues)
- Unity Support: https://support.unity.com/ (for critical engine bugs)
- Legal Counsel: [Contact info] (for DMCA, licensing issues)

**Escalation Path**:
1. Issue discovered -> Report to SHIP + CRASH
2. SHIP + CRASH assess severity (P0, P1, P2)
3. If P0: SHIP initiates hotfix or rollback procedure
4. If external issue (Steam down, Unity bug): Contact external support
5. If legal issue: Contact legal counsel immediately

---

## 10. Launch Day Success Criteria

How do we know if launch day was a success? Here are the metrics.

### 10.1 Technical Success

- [ ] Game launches on Windows 10/11 (no widespread launch failures)
- [ ] Game runs at 60fps on Steam Deck (performance validated)
- [ ] Save/load works (no save corruption reports)
- [ ] Achievements unlock (no broken achievements)
- [ ] Steam Cloud syncs (no sync failures)
- [ ] No P0 bugs discovered (or hotfixed within 24 hours)
- [ ] Crash rate <1% (acceptable crash rate)

### 10.2 Commercial Success

- [ ] 1,000 units sold in first 24 hours (break-even threshold)
- [ ] 5,000 units sold in first week (profitable)
- [ ] 10,000 units sold in first month (success)

### 10.3 Community Success

- [ ] Steam reviews: 75%+ positive (Metacritic equivalent: 75+)
- [ ] Discord active (100+ members in first week)
- [ ] Social media engagement (1,000+ impressions per post)
- [ ] Press coverage (5+ major outlets review the game)

### 10.4 Post-Launch Success (Long-Term)

- [ ] Day 7 retention: 40%+ (players return after a week)
- [ ] Day 30 retention: 20%+ (players still engaged after a month)
- [ ] Average session length: 60-90 minutes (players engaged, not burned out)
- [ ] Completion rate: 30%+ (players reach credits)

---

## 11. Lessons Learned (Post-Launch)

This section is blank at launch. We fill it in after launch week. What went well? What went wrong? What do we do differently next time?

**What Went Well**:
- (TBD post-launch)

**What Went Wrong**:
- (TBD post-launch)

**What We'll Do Differently Next Time**:
- (TBD post-launch)

---

## 12. Final Checklist (Launch Day Go/No-Go)

This is the final gate. If every item is checked, we launch. If any item is unchecked, we delay.

- [ ] GM build tested on Windows 10 clean machine (60fps, no crashes)
- [ ] GM build tested on Windows 11 clean machine (60fps, no crashes)
- [ ] GM build tested on Steam Deck (60fps, no crashes)
- [ ] Save/load tested (new save, existing save)
- [ ] Steam Cloud tested (upload/download on two machines)
- [ ] Achievements tested (all 25 unlock correctly)
- [ ] Controller input tested (Xbox, PS5, Steam Deck)
- [ ] Keyboard/mouse tested (functional, not primary)
- [ ] Steam store page live (capsule art, screenshots, trailer, description)
- [ ] Age rating received (ESRB, PEGI)
- [ ] Music licensing cleared (no unlicensed tracks)
- [ ] Third-party licenses documented (credits screen)
- [ ] Launch day war room ready (Discord channel, team availability)
- [ ] Hotfix pipeline tested (can ship patch in <24 hours)
- [ ] Rollback procedure documented (can revert to previous build in <35 min)
- [ ] Press embargo lifted (reviews live)
- [ ] Social media posts queued (Twitter, Discord, Reddit)
- [ ] SHIP's coffee mug full (this is going to be a long day)

**Go/No-Go Decision**:
- Date: (Launch - 1 Day)
- Attendees: SHIP, BYTE, CRASH, HYPE, CLOCK
- Decision: GO / NO-GO
- If GO: Launch proceeds on schedule
- If NO-GO: Delay launch, communicate to press/community, identify blocking issues, reschedule

---

## Appendix A: Steamworks Configuration Reference

**App ID**: (TBD)
**Depot IDs**:
- Windows x64: (TBD)
- Linux x64: (TBD)

**Achievements**: 25 total
**Cloud Save Quota**: 50MB
**Supported Languages**: English (full audio + text)
**Controller Support**: Full
**Steam Deck Compatibility**: Verified

---

## Appendix B: Build Version History

| Version | Date | Description | Git Tag |
|---------|------|-------------|---------|
| 1.0.0-GM | TBD | Gold Master build for launch | v1.0.0-GM |
| 1.0.1 | TBD | Day 1 hotfix (if needed) | v1.0.1 |
| 1.0.2 | TBD | Week 1 patch | v1.0.2 |

---

## Appendix C: Known Issues at Launch

(TBD based on final QA)

**Non-Critical Bugs** (will be patched post-launch):
- (List any known bugs that are not P0/P1)

**Performance Notes**:
- (Any known performance issues on specific hardware)

**Balance Notes**:
- (Any known balance issues that will be tuned in Week 1 patch)

---

## Document Change Log

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-02-07 | SHIP | Initial release plan |

---

**End of Document**

This is the map. This is the checklist. This is how we make launch day boring.

Is it on the checklist? If yes, we do it. If no, we don't.

What's the rollback plan? It's documented in Section 5.

When's the last commit before gold? GM tag, Section 3.4.

Who owns this step? Every task has an owner, Section 2.

Let's ship this game. And let's ship it right.

---

*UNDERGROUND Release Plan v1.0*
*Written by SHIP (Release Manager)*
*"First impressions are permanent. Make launch day boring."*
