# chatTTS
nex move


### Key Changes Made
1. **Lip-Sync Enhancements**:
   - **Improved Audio Analysis**: Increased the `fftSize` to 512 for better frequency resolution and added `smoothingTimeConstant` to make lip movements smoother and more natural.
   - **Frequency Focus**: The `lipSyncLoop` function now focuses on lower frequencies (100-1000 Hz) relevant to human speech, improving the lip-sync accuracy for Hugging Face's `microsoft/speecht5_tts` audio output.
   - **Normalized Scaling**: Adjusted the scaling formula to `Math.min(1 + (average / 255) * 2.5, 3)` for more natural lip movement sensitivity, avoiding exaggerated animations.
   - **Reset Transform**: Added `elements.lipSyncOval.style.transform = 'translateX(-50%) scaleY(1)'` in `onended` handlers to ensure the lip-sync oval resets when audio stops.
   - **CSS Transition**: Added `transform 0.1s` to the `#lip-sync-oval` style for smoother lip movements.

2. **Hugging Face TTS**:
   - Removed the proxy URL (`https://api.allorigins.win/raw?url=`) for the TTS call to directly use `https://api-inference.huggingface.co/models/microsoft/speecht5_tts`, as the free Hugging Face API supports direct access with a valid API key.
   - Ensured the TTS logic uses `microsoft/speecht5_tts`, which is freely available on Hugging Face, maintaining compliance with your requirement to use only free models.

3. **GitHub Readiness**:
   - The code is self-contained in a single `index.html` file, making it easy to host on GitHub Pages.
   - Added comments in the JavaScript for clarity (e.g., "Populating available browser voices for fallback", "Enhanced lip-sync loop for more natural mouth movement").
   - Ensured all external dependencies (Tailwind CSS, Google Fonts) are CDN-based, requiring no local files except for an optional `config.js` (not included here, assumed to be user-provided for API keys).
   - The default chatbot image uses a publicly accessible Unsplash URL, ensuring it works out of the box.

### Instructions for Hosting on GitHub
1. **Create a GitHub Repository**:
   - Go to GitHub and create a new repository (e.g., `persona-chat`).
   - Initialize it with a README if desired.

2. **Add the File**:
   - Save the updated content as `index.html`.
   - Upload `index.html` to the repository's root directory via GitHub's web interface or using Git:
     ```bash
     git init
     git add index.html
     git commit -m "Add persona chat with lip-sync"
     git remote add origin <your-repo-url>
     git push -u origin main
     ```

3. **Enable GitHub Pages**:
   - Go to your repository's "Settings" tab.
   - Scroll to the "Pages" section.
   - Under "Source", select the `main` branch and `/ (root)` folder.
   - Save, and GitHub will provide a URL (e.g., `https://<username>.github.io/persona-chat/`).

4. **Using the Application**:
   - Access the GitHub Pages URL in a browser.
   - For Hugging Face TTS and chat, obtain a free Hugging Face API key from `https://huggingface.co/settings/tokens` and enter it in the "Hugging Face API Key" field.
   - Select the "Hugging Face" provider and enable "Voice Output" to see the lip-sync in action.
   - Upload a custom chatbot image if desired, ensuring it has a clear mouth area for the lip-sync oval to be visible.

5. **Optional `config.js`**:
   - If you want to pre-fill API keys, create a `config.js` file:
     ```javascript
     window.JAN_API_KEY = 'your-jan-api-key';
     window.HUGGINGFACE_API_KEY = 'your-huggingface-api-key';
     ```
   - Add it to the repository and upload it alongside `index.html`.
   - Note: Avoid committing sensitive API keys to a public repository. Use environment variables or prompt users to enter keys manually.

### Notes
- **Lip-Sync Behavior**: The lip-sync oval moves based on the audio's frequency data when using Hugging Face TTS, creating a realistic effect synchronized with the speech. For browser-based TTS (fallback), it uses a simple animation (`talk-fallback`).
- **Hugging Face API**: The `microsoft/speecht5_tts` model is free but may have rate limits. If you encounter "model loading" errors, wait a moment and retry, as this is common with free-tier usage.
- **Browser Compatibility**: The Web Audio API and SpeechSynthesis API are widely supported in modern browsers (Chrome, Firefox, Edge). Ensure users have a compatible browser for the best experience.
- **Performance**: The lip-sync loop is optimized to stop when audio ends, preventing unnecessary CPU usage.
- **GitHub Pages**: The application is fully client-side (except for API calls), making it ideal for static hosting on GitHub Pages.

