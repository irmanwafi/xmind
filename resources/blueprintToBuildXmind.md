# 🧠 GitHub Copilot Blueprint — Build `+page.svelte` Interactive Tutorial Viewer

## 🎯 Objective
Create a clean, compact, Apple-style tutorial page to guide users from raw data → ChatGPT → Markdown → XMind → SmartArt. Build in SvelteKit with Tailwind and Poppins.

---

## 📦 Files & Links (Copilot: use these in UI)

### 📊 Raw Data & Prompts
- Google Sheet with dummy data & ChatGPT prompts:  
  https://docs.google.com/spreadsheets/d/1xGabr65sYrTTuZb2URsm6wfHUPbXdK9ULOBId5kt3hE/edit?usp=sharing

### 💬 Prompt Templates (Add copy buttons)
- `chatGPT-prompt-1.md`
- `chatGPT-prompt-2.md`
- `chatGPT-prompt-3.md`

### 🧾 Markdown Outputs (Show as `<pre><code>`, with copy)
- `melaka-prompt-1.md`
- `melaka-prompt-2.md`
- `plus-prompt-3.md`

### 🧠 XMind Visual
- Online XMind web map:
  https://xmind.ai/share/ofCt9Dkk?xid=Wp7vW9UI  
- Folder with XMind + other assets:  
  https://drive.google.com/drive/folders/1yBkI2Wea95dlJ2svK4vAYr_4YONYvG5N?usp=drive_link

### 📥 SmartArt Output (PPTX Download)
- Google Slides (downloadable):
  https://docs.google.com/presentation/d/1_W5DeYmnTuMOX-RluyshK26ndUQrwGfL/edit?usp=drive_link&ouid=101657559488423790022&rtpof=true&sd=true

### 🎥 Tutorial Video
- Google Drive video:
  https://drive.google.com/file/d/1yicW1DLJY_11eLrmV6b1rLsqF-HkGaau/view?usp=sharing

---

## 🧱 Page Layout (Copilot: build in this order)

1. **Header**
   - Title: “Convert Raw Data to SmartArt”
   - Subtitle: “Interactive flow from prompt to PowerPoint”
   - Poppins font, centered, large

2. **Visual Step Cards (Apple-style)**
   - 5 horizontal or stacked cards:
     1. Import raw data → [Google Sheet]
     2. Use ChatGPT → `chatGPT-prompt-[1-3].md`
     3. Convert to Markdown → `melaka/plus-prompt.md`
     4. Import to XMind → [XMind Web]
     5. Finalize in SmartArt → [Download PPTX]

3. **Step-by-Step Guide**
   - Use `<details>` for each step
   - Each includes links and copy buttons:
     - Prompts to copy
     - Markdown outputs to copy
     - External links to Google tools

4. **Markdown Viewer**
   - Render `melaka-prompt-1.md`, `melaka-prompt-2.md`, `plus-prompt-3.md`
   - Each with copy-to-clipboard
   - Use `<pre><code>` + Tailwind spacing

5. **XMind Section**
   - Show PNG or embed link
   - Link to: https://xmind.ai/share/ofCt9Dkk?xid=Wp7vW9UI

6. **SmartArt Section**
   - Button: “Download SmartArt PPTX”
   - Link to: https://docs.google.com/presentation/d/1_W5DeYmnTuMOX-RluyshK26ndUQrwGfL/edit?usp=drive_link

7. **Video**
   - Embed or link: https://drive.google.com/file/d/1yicW1DLJY_11eLrmV6b1rLsqF-HkGaau/view

8. **Footer (optional)**
   - Show tutorial folder link:
     https://drive.google.com/drive/folders/1yBkI2Wea95dlJ2svK4vAYr_4YONYvG5N

---

## 🧑‍💻 Copilot Style Rules
- Use Tailwind CSS utility classes only
- Global font: `'Poppins', sans-serif`
- Responsive design: mobile first
- `max-w-screen-lg` for readable width
- Clean, uncluttered layout
- Semantic HTML: `<section>`, `<details>`, `<header>`, `<footer>`
- Add copy button with clipboard logic (per markdown/prompt)

---

This prompt tells Copilot how to build a fully interactive, visually clean, and logic-driven tutorial viewer page in SvelteKit. All links, files, and flow steps are included.
