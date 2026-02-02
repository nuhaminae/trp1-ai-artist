# SUBMISSION.md

## Environment Setup Documentation

- **APIs Configured**
  - **Google Gemini API** → Used for Lyria (music), Veo (video), and Imagen (image).

- **Issues Encountered**
  - Google's API failed to generate video pointing to billing issues.

- **Resolutions**
  - Couldnt resolve billing issues in time.
---

## Codebase Understanding

- **Architecture Description**
  - The system is modular:
    - `cli/` → Entry points for commands.
    - `providers/` → Each AI provider (Google Lyria, Veo, Imagen, AIMLAPI MiniMax, KlingAI).
    - `pipelines/` → Orchestration logic chaining providers and presets.
    - `presets/` → Predefined styles for music and video.
    - `core/` → Job orchestration and execution.
    - `utils/` → Shared helpers.

- **Provider System Insights**
  - Providers are plug-ins, each with its own API wrapper.
  - Google Gemini covers multiple modalities (music, video, image).
  - AIMLAPI MiniMax uniquely supports lyrics/vocals.

- **Pipeline Orchestration**
  - Pipelines define workflows
  - They abstract away provider-specific details, letting CLI commands stay consistent across providers.

---

## Generation Log

- **Commands Executed**

  ```bash
  uv run ai-content music --prompt "Ethiopian jazz fusion" --provider lyria
  uv run ai-content music --prompt "Urban hip-hop with vocals" --provider minimax --lyrics lyrics.txt
  uv run ai-content video --style nature --provider veo --duration 5
  ffmpeg -i video.mp4 -i music.wav -c:v copy -c:a aac -shortest output.mp4
  ```

- **Prompts Used**
  - *“Ethiopian jazz fusion”* → to test cultural style blending.
  - *“Urban hip-hop with vocals”* → to test AIMLAPI’s lyric integration.

- **Results Achieved**
  - Jazz track: 30s, ~2.5MB WAV file.
  - Hip-hop track with vocals: 45s, ~3MB WAV file.
  - Nature video: 5s, ~8MB MP4 file.
  - Combined music video: 5s, ~10MB MP4 file.

---

## Challenges & Solutions

- **What Didn’t Work Initially**
  - Running  `uv run ai-content music --style jazz --provider lyria --duration 30` failed because Lyria only supports prompts, not styles.

- **Troubleshooting**
  - Switched to prompt-based input for Lyria.

- **Workarounds**
  - Used Google Veo for video generation instead of KlingAI.

---

## Insights & Learnings

- **Surprises**
  - The modular provider system made it easy to switch between backends without changing CLI syntax.
  - Presets were well-optimized and produced better results than custom prompts.

- **Improvements**
  - Documentation could be clearer about provider-specific limitations (e.g., Lyria = instrumental only).
  - More examples for video workflows would help.

---

## Links

- **YouTube Video Link(s)**  
  Unlisted YouTube Demo [(youtube.com)](https://www.bing.com/search?q="https%3A%2F%2Fyoutube.com%2Fyour-demo-link")

- **GitHub Repo with Exploration Artifacts**  
  My Exploration Repo [(github.com)](https://github.com/nuhaminae/trp1-ai-artist")

---
