# 🎙️ NotebookLM Video Research Skill

> A Claude skill that automates NotebookLM notebook creation from YouTube videos — research featured people, add sources, and generate Audio Overviews automatically.

[![Claude Skill](https://img.shields.io/badge/Claude-Skill-blueviolet)](https://support.claude.com/en/articles/12512180-using-skills-in-claude)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 🎯 What It Does

Give Claude a YouTube link, and it will:

1. **Extract** people mentioned in the video
2. **Research** their backgrounds via web search
3. **Create** a NotebookLM notebook with:
   - YouTube video as a source (transcript auto-extracted)
   - Research document as additional context
4. **Generate** an Audio Overview podcast

Perfect for turning interviews, talks, and documentaries into listen-on-the-go podcasts.

## 📺 Example

**Input:**
```
Use the notebooklm video research skill to prepare audio overview of this video:
https://www.youtube.com/watch?v=0nlNX94FcUE
```

**Output:**
- NotebookLM notebook with full video transcript
- Research on Sergey Brin's background and recent work
- Audio Overview podcast ready to listen

## 🚀 Installation

### Prerequisites

- [Claude Desktop](https://claude.ai/download) app
- Google account logged into [NotebookLM](https://notebooklm.google.com/)
- Chrome browser

### Step 1: Enable Chrome Control

1. In Claude Desktop, go to **Settings → Connectors**
2. Enable **"Control Chrome"** connector

### Step 2: Enable JavaScript for Apple Events (Mac only)

1. Open Chrome
2. Go to **View → Developer** menu
3. Enable **"Allow JavaScript from Apple Events"**

### Step 3: Install the Skill

**Option A: Download and install manually**

1. Download this repository as ZIP
2. Extract to your Claude skills folder
3. Follow [Anthropic's skill installation guide](https://support.claude.com/en/articles/12512180-using-skills-in-claude#h_a4222fa77b)

**Option B: Clone with git**

```bash
cd ~/Library/Application\ Support/Claude/skills  # Mac
# or
cd %APPDATA%\Claude\skills  # Windows

git clone https://github.com/YOUR_USERNAME/notebooklm-video-research.git
```

## 💬 Usage

Just tell Claude:

```
Use the notebooklm video research skill to prepare audio overview of this video: [YouTube URL]
```

Or more casually:

```
Create a NotebookLM notebook for this video: [YouTube URL]
```

### Tips

- Works with **Haiku** model for faster/cheaper runs
- Let it run in the background — takes a few minutes
- Make sure you're logged into NotebookLM in Chrome before starting

## 📁 Files

```
notebooklm-video-research/
├── SKILL.md                    # Main skill instructions for Claude
├── README.md                   # This file
└── references/
    └── notebooklm_ui_guide.md  # UI element reference for automation
```

## 🔧 How It Works

The skill uses a **screenshot-first automation** approach:

```
📸 Screenshot → 👀 Analyze → 🎯 Target → 🖱️ Execute → 📸 Verify
```

This is crucial because NotebookLM has multiple similar-looking input fields. Without visual verification, automation often targets the wrong element.

### Key Technical Detail

NotebookLM uses Angular, so simple `.value = 'text'` doesn't work. The skill uses proper event dispatching:

```javascript
var setter = Object.getOwnPropertyDescriptor(
    HTMLTextAreaElement.prototype, 'value'
).set;
setter.call(textarea, 'content');
textarea.dispatchEvent(new Event('input', {bubbles: true}));
```

## ⏱️ Expected Wait Times

| Action | Time |
|--------|------|
| Video research | 1-2 min |
| NotebookLM automation | 2-3 min |
| Audio Overview generation | 5-10 min |

## 🤝 Contributing

Found a bug? Have an improvement? PRs welcome!

Ideas for extensions:
- Generate slide decks from video content
- Add multiple videos to one notebook
- Include additional web sources automatically
- Create structured notes instead of/alongside audio

## 📝 License

MIT — use freely, modify as needed, share with others.

## 🙏 Credits

- Built with [Claude](https://claude.ai) by Anthropic
- Uses [NotebookLM](https://notebooklm.google.com/) by Google

---

**Questions?** Open an issue or reach out on [Twitter/X](https://twitter.com/YOUR_HANDLE).
