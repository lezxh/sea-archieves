# sea-archieves

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <meta name="theme-color" content="#0a1628">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <title>Sea Archives 💗</title>
    <style>
        :root {
            --bg: #0a1628;
            --surface: #0f1f3a;
            --surface2: #162d50;
            --primary: #4da6ff;
            --primary-glow: #7ec8ff;
            --accent: #ff7eb3;
            --accent2: #ffb8d4;
            --text: #e0eaf5;
            --text2: #7b93b0;
            --danger: #ff6b7a;
            --success: #4dd4ac;
            --border: #1a3355;
            --radius: 18px;
            --radius-sm: 12px;
        }
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: var(--bg);
            background-image: 
                radial-gradient(ellipse at 20% 20%, rgba(77, 166, 255, 0.06) 0%, transparent 50%),
                radial-gradient(ellipse at 80% 80%, rgba(255, 126, 179, 0.06) 0%, transparent 50%);
            color: var(--text);
            height: 100vh;
            height: 100dvh;
            overflow: hidden;
            -webkit-tap-highlight-color: transparent;
        }
        /* ========== SCREENS ========== */
        .screen {
            display: none;
            height: 100%;
            flex-direction: column;
        }
        .screen.active {
            display: flex;
        }
        /* ========== CHARACTER SELECT ========== */
        #charSelectScreen {
            padding: 20px;
            overflow-y: auto;
        }
        .top-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 24px;
            position: sticky;
            top: 0;
            background: var(--bg);
            padding: 16px 0;
            z-index: 10;
            backdrop-filter: blur(10px);
        }
        .logo {
            font-size: 1.7rem;
            font-weight: 800;
            background: linear-gradient(135deg, #4da6ff, #7ec8ff, #ff7eb3);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            letter-spacing: -0.5px;
        }
        .logo-emoji {
            font-size: 1.8rem;
        }
        .btn {
            border: none;
            padding: 12px 20px;
            border-radius: var(--radius-sm);
            font-weight: 600;
            font-size: 0.9rem;
            cursor: pointer;
            transition: all 0.25s;
            display: flex;
            align-items: center;
            gap: 6px;
        }
        .btn:active { transform: scale(0.96); }
        .btn-primary {
            background: linear-gradient(135deg, #4da6ff, #7ec8ff);
            color: #0a1628;
            box-shadow: 0 4px 20px rgba(77, 166, 255, 0.25);
        }
        .btn-secondary {
            background: var(--surface2);
            color: var(--text);
            border: 1px solid var(--border);
        }
        .btn-small {
            padding: 8px 14px;
            font-size: 0.8rem;
        }
        .btn-icon {
            background: transparent;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            padding: 8px;
            border-radius: 50%;
            width: 44px;
            height: 44px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--text2);
            transition: all 0.2s;
        }
        .btn-icon:hover, .btn-icon:active {
            color: var(--primary);
            background: rgba(77, 166, 255, 0.1);
        }
        .char-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(155px, 1fr));
            gap: 16px;
            padding-bottom: 40px;
        }
        .char-card {
            background: var(--surface);
            border-radius: var(--radius);
            padding: 20px 16px;
            cursor: pointer;
            transition: all 0.3s;
            border: 2px solid transparent;
            text-align: center;
            position: relative;
            overflow: hidden;
        }
        .char-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 3px;
            background: linear-gradient(90deg, #4da6ff, #ff7eb3);
            opacity: 0;
            transition: opacity 0.3s;
        }
        .char-card:hover::before, .char-card:active::before {
            opacity: 1;
        }
        .char-card:hover, .char-card:active {
            border-color: rgba(77, 166, 255, 0.3);
            box-shadow: 0 8px 40px rgba(77, 166, 255, 0.12);
            transform: translateY(-3px);
        }
        .char-avatar {
            width: 75px;
            height: 75px;
            border-radius: 50%;
            margin: 0 auto 12px;
            object-fit: cover;
            background: var(--surface2);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2.2rem;
            border: 3px solid var(--border);
            transition: border-color 0.3s;
        }
        .char-card:hover .char-avatar {
            border-color: rgba(77, 166, 255, 0.5);
        }
        .char-avatar img {
            width: 100%;
            height: 100%;
            border-radius: 50%;
            object-fit: cover;
        }
        .char-name {
            font-weight: 700;
            font-size: 1rem;
            margin-bottom: 4px;
            color: var(--text);
        }
        .char-role {
            font-size: 0.75rem;
            color: var(--text2);
        }
        .char-messages-badge {
            font-size: 0.65rem;
            color: var(--primary-glow);
            margin-top: 6px;
        }
        .char-delete {
            position: absolute;
            top: 8px;
            right: 8px;
            background: rgba(255, 107, 122, 0.9);
            border: none;
            color: white;
            width: 26px;
            height: 26px;
            border-radius: 50%;
            font-size: 0.8rem;
            cursor: pointer;
            opacity: 0;
            transition: opacity 0.2s;
            z-index: 2;
        }
        .char-card:hover .char-delete, .char-card:active .char-delete {
            opacity: 1;
        }
        .empty-chars {
            text-align: center;
            padding: 60px 20px;
            color: var(--text2);
            grid-column: 1 / -1;
        }
        .empty-chars .emoji {
            font-size: 5rem;
            display: block;
            margin-bottom: 16px;
            animation: float 3s ease-in-out infinite;
        }
        @keyframes float {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }
        .empty-chars h3 {
            font-size: 1.3rem;
            color: var(--text);
            margin-bottom: 8px;
        }
        /* ========== CHAT SCREEN ========== */
        #chatScreen {
            height: 100%;
        }
        .chat-header {
            background: var(--surface);
            padding: 14px 16px;
            display: flex;
            align-items: center;
            gap: 12px;
            border-bottom: 1px solid var(--border);
            position: sticky;
            top: 0;
            z-index: 10;
            backdrop-filter: blur(10px);
        }
        .chat-header .char-avatar {
            width: 44px;
            height: 44px;
            margin: 0;
            font-size: 1.4rem;
            flex-shrink: 0;
        }
        .chat-header-info {
            flex: 1;
            min-width: 0;
        }
        .chat-header-name {
            font-weight: 700;
            font-size: 1.05rem;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        .chat-header-status {
            font-size: 0.72rem;
            color: var(--success);
            display: flex;
            align-items: center;
            gap: 4px;
        }
        .chat-header-status::before {
            content: '';
            width: 7px;
            height: 7px;
            border-radius: 50%;
            background: var(--success);
            animation: pulse 2s infinite;
        }
        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.4; }
        }
        .chat-messages {
            flex: 1;
            overflow-y: auto;
            padding: 16px;
            display: flex;
            flex-direction: column;
            gap: 12px;
            -webkit-overflow-scrolling: touch;
            background: 
                radial-gradient(ellipse at 50% 0%, rgba(77, 166, 255, 0.03) 0%, transparent 60%);
        }
        .message {
            display: flex;
            gap: 10px;
            max-width: 88%;
            animation: fadeIn 0.35s ease;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .message.user {
            align-self: flex-end;
            flex-direction: row-reverse;
        }
        .message-avatar {
            width: 34px;
            height: 34px;
            border-radius: 50%;
            flex-shrink: 0;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.9rem;
            background: var(--surface2);
            border: 1px solid var(--border);
        }
        .message-avatar img {
            width: 100%;
            height: 100%;
            border-radius: 50%;
            object-fit: cover;
        }
        .message-bubble {
            padding: 12px 16px;
            border-radius: 20px;
            font-size: 0.95rem;
            line-height: 1.55;
            word-break: break-word;
        }
        .message.user .message-bubble {
            background: linear-gradient(135deg, #4da6ff, #3d8ed9);
            color: white;
            border-bottom-right-radius: 6px;
            box-shadow: 0 2px 12px rgba(77, 166, 255, 0.2);
        }
        .message.ai .message-bubble {
            background: var(--surface);
            color: var(--text);
            border-bottom-left-radius: 6px;
            border: 1px solid var(--border);
        }
        .message .timestamp {
            font-size: 0.65rem;
            color: var(--text2);
            margin-top: 5px;
            text-align: right;
        }
        .typing-indicator {
            display: none;
            align-items: center;
            gap: 5px;
            padding: 12px 18px;
            background: var(--surface);
            border-radius: 20px;
            align-self: flex-start;
            border: 1px solid var(--border);
            border-bottom-left-radius: 6px;
        }
        .typing-indicator.active {
            display: flex;
        }
        .typing-dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background: var(--primary-glow);
            animation: bounce 1.4s infinite ease-in-out;
        }
        .typing-dot:nth-child(1) { animation-delay: 0s; }
        .typing-dot:nth-child(2) { animation-delay: 0.2s; }
        .typing-dot:nth-child(3) { animation-delay: 0.4s; }
        @keyframes bounce {
            0%, 80%, 100% { transform: scale(0.5); opacity: 0.3; }
            40% { transform: scale(1); opacity: 1; }
        }
        .chat-input-area {
            background: var(--surface);
            padding: 12px 16px;
            display: flex;
            gap: 10px;
            border-top: 1px solid var(--border);
            align-items: flex-end;
        }
        .chat-input-area textarea {
            flex: 1;
            border: 1px solid var(--border);
            background: var(--surface2);
            color: var(--text);
            border-radius: 24px;
            padding: 12px 18px;
            font-size: 0.95rem;
            resize: none;
            max-height: 120px;
            font-family: inherit;
            outline: none;
            transition: border-color 0.2s;
        }
        .chat-input-area textarea:focus {
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(77, 166, 255, 0.1);
        }
        .chat-input-area textarea::placeholder {
            color: var(--text2);
        }
        .send-btn {
            background: linear-gradient(135deg, #4da6ff, #7ec8ff);
            border: none;
            color: #0a1628;
            width: 48px;
            height: 48px;
            border-radius: 50%;
            font-size: 1.3rem;
            cursor: pointer;
            flex-shrink: 0;
            transition: all 0.25s;
            font-weight: 700;
        }
        .send-btn:active { transform: scale(0.88); }
        .send-btn:disabled {
            background: var(--surface2);
            color: var(--text2);
            cursor: not-allowed;
        }
        /* ========== CREATE/EDIT MODAL ========== */
        .modal-overlay {
            display: none;
            position: fixed;
            inset: 0;
            background: rgba(5, 12, 25, 0.85);
            backdrop-filter: blur(6px);
            z-index: 100;
            align-items: flex-end;
            justify-content: center;
        }
        .modal-overlay.active {
            display: flex;
        }
        .modal {
            background: var(--surface);
            border-radius: 28px 28px 0 0;
            padding: 28px 20px;
            width: 100%;
            max-width: 500px;
            max-height: 88vh;
            overflow-y: auto;
            animation: slideUp 0.35s ease;
            border-top: 2px solid var(--border);
        }
        @keyframes slideUp {
            from { transform: translateY(100%); }
            to { transform: translateY(0); }
        }
        .modal h2 {
            font-size: 1.5rem;
            margin-bottom: 22px;
            text-align: center;
            background: linear-gradient(135deg, #4da6ff, #ff7eb3);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        .form-group {
            margin-bottom: 16px;
        }
        .form-group label {
            display: block;
            font-size: 0.82rem;
            font-weight: 600;
            color: var(--primary-glow);
            margin-bottom: 6px;
            text-transform: uppercase;
            letter-spacing: 0.8px;
        }
        .form-group input, .form-group textarea, .form-group select {
            width: 100%;
            padding: 12px 16px;
            border-radius: var(--radius-sm);
            border: 1px solid var(--border);
            background: var(--surface2);
            color: var(--text);
            font-size: 0.95rem;
            font-family: inherit;
            outline: none;
            transition: all 0.2s;
        }
        .form-group textarea {
            resize: vertical;
            min-height: 80px;
        }
        .form-group input:focus, .form-group textarea:focus {
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(77, 166, 255, 0.08);
        }
        .form-group input::placeholder, .form-group textarea::placeholder {
            color: #4a6080;
        }
        .image-upload-area {
            text-align: center;
        }
        .image-preview {
            width: 100px;
            height: 100px;
            border-radius: 50%;
            object-fit: cover;
            margin: 0 auto 12px;
            display: block;
            background: var(--surface2);
            border: 3px solid var(--border);
            transition: border-color 0.3s;
        }
        .image-preview:hover {
            border-color: var(--primary);
        }
        .image-placeholder {
            width: 100px;
            height: 100px;
            border-radius: 50%;
            margin: 0 auto 12px;
            background: var(--surface2);
            border: 3px dashed var(--border);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2.5rem;
            cursor: pointer;
            transition: all 0.3s;
        }
        .image-placeholder:hover {
            border-color: var(--primary);
            background: rgba(77, 166, 255, 0.05);
        }
        .modal-buttons {
            display: flex;
            gap: 10px;
            margin-top: 24px;
        }
        .modal-buttons .btn {
            flex: 1;
            justify-content: center;
        }
        /* ========== SETTINGS BAR ========== */
        .settings-bar {
            display: flex;
            gap: 8px;
            padding: 10px 0;
            margin-bottom: 8px;
            align-items: center;
            flex-wrap: wrap;
        }
        .api-key-input {
            background: var(--surface2);
            border: 1px solid var(--border);
            color: var(--text);
            padding: 10px 14px;
            border-radius: 24px;
            font-size: 0.8rem;
            width: 190px;
            outline: none;
            transition: all 0.2s;
        }
        .api-key-input:focus {
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(77, 166, 255, 0.08);
        }
        .api-key-input::placeholder {
            color: #4a6080;
        }
        .api-link {
            font-size: 0.7rem;
            color: var(--text2);
            align-self: center;
            text-decoration: none;
        }
        .api-link a {
            color: var(--accent2);
            text-decoration: underline;
        }
        /* Scrollbar */
        ::-webkit-scrollbar { width: 4px; }
        ::-webkit-scrollbar-track { background: transparent; }
        ::-webkit-scrollbar-thumb { background: var(--border); border-radius: 4px; }
    </style>
</head>
<body>

    <!-- ==================== CHARACTER SELECT SCREEN ==================== -->
    <div class="screen active" id="charSelectScreen">
        <div class="top-bar">
            <span class="logo"><span class="logo-emoji">🌊</span> Sea Archives <span style="font-size:1.2rem;">💗</span></span>
            <button class="btn btn-primary" onclick="openCreateModal()">✨ New Character</button>
        </div>
        <div class="settings-bar">
            <input type="password" class="api-key-input" id="apiKeyInput" placeholder="🔑 Groq API Key">
            <button class="btn btn-small btn-secondary" onclick="saveApiKey()">💾 Save</button>
            <span class="api-link">Free key → <a href="https://console.groq.com" target="_blank">console.groq.com</a></span>
        </div>
        <div class="char-grid" id="charGrid"></div>
    </div>

    <!-- ==================== CHAT SCREEN ==================== -->
    <div class="screen" id="chatScreen">
        <div class="chat-header">
            <button class="btn-icon" onclick="goBack()">←</button>
            <div class="char-avatar" id="chatCharAvatar">🌊</div>
            <div class="chat-header-info">
                <div class="chat-header-name" id="chatCharName">Sea Archives</div>
                <div class="chat-header-status" id="chatCharStatus">Connected</div>
            </div>
            <button class="btn-icon" onclick="editCurrentChar()" title="Edit character">⚙️</button>
            <button class="btn-icon" onclick="clearCurrentChat()" title="Clear chat history">🗑️</button>
        </div>
        <div class="chat-messages" id="chatMessages">
            <div class="typing-indicator" id="typingIndicator">
                <div class="typing-dot"></div>
                <div class="typing-dot"></div>
                <div class="typing-dot"></div>
            </div>
        </div>
        <div class="chat-input-area">
            <textarea id="messageInput" rows="1" placeholder="Write your story..." onkeydown="handleKeyDown(event)"></textarea>
            <button class="send-btn" id="sendBtn" onclick="sendMessage()">➤</button>
        </div>
    </div>

    <!-- ==================== CREATE/EDIT MODAL ==================== -->
    <div class="modal-overlay" id="modalOverlay">
        <div class="modal" id="modalContent">
            <h2 id="modalTitle">🌊 New Character</h2>
            <form id="charForm" onsubmit="handleFormSubmit(event)">
                <div class="image-upload-area">
                    <img class="image-preview" id="imagePreview" src="" alt="Preview" style="display:none;">
                    <div class="image-placeholder" id="imagePlaceholder" onclick="document.getElementById('imageInput').click()">📷</div>
                </div>
                <div class="form-group">
                    <label>📸 Character Image</label>
                    <input type="file" id="imageInput" accept="image/*" onchange="previewImage(event)" style="display:none;">
                    <button type="button" class="btn btn-small btn-secondary" onclick="document.getElementById('imageInput').click()" style="width:100%;justify-content:center;">Choose Image</button>
                </div>
                <div class="form-group">
                    <label>✨ Name *</label>
                    <input type="text" id="charNameInput" placeholder="e.g. Caspian, the Tide Walker" required maxlength="40">
                </div>
                <div class="form-group">
                    <label>🎭 Role / Title</label>
                    <input type="text" id="charRoleInput" placeholder="e.g. Ocean Spirit, Storm Pirate" maxlength="60">
                </div>
                <div class="form-group">
                    <label>📜 Personality & Backstory *</label>
                    <textarea id="charPersonalityInput" rows="4" placeholder="Describe their personality, history, manner of speaking, knowledge, quirks... The AI will use this to stay in character." required></textarea>
                </div>
                <div class="form-group">
                    <label>💬 Example Dialogue</label>
                    <textarea id="charExampleInput" rows="3" placeholder="&quot;The tides have told me of your coming, dear traveler. Come, rest by the shore.&quot;"></textarea>
                </div>
                <input type="hidden" id="editCharId" value="">
                <div class="modal-buttons">
                    <button type="button" class="btn btn-secondary" onclick="closeModal()">Cancel</button>
                    <button type="submit" class="btn btn-primary">💾 Save Character</button>
                </div>
            </form>
        </div>
    </div>

    <script>
        // ==================== APP STATE ====================
        const STORAGE_KEY = 'seaarchives_data';
        let appData = {
            apiKey: '',
            characters: [],
            currentCharId: null
        };

        // ==================== INIT ====================
        function loadData() {
            const saved = localStorage.getItem(STORAGE_KEY);
            if (saved) {
                appData = JSON.parse(saved);
            }
            appData.characters.forEach(c => {
                if (!c.messages) c.messages = [];
            });
            document.getElementById('apiKeyInput').value = appData.apiKey || '';
        }

        function saveData() {
            localStorage.setItem(STORAGE_KEY, JSON.stringify(appData));
        }

        function saveApiKey() {
            appData.apiKey = document.getElementById('apiKeyInput').value.trim();
            saveData();
            const msg = appData.apiKey ? '✅ API Key saved! Ready to sail.' : '🔑 API Key cleared.';
            showToast(msg);
        }

        // ==================== TOAST ====================
        function showToast(message) {
            let toast = document.getElementById('toast');
            if (!toast) {
                toast = document.createElement('div');
                toast.id = 'toast';
                toast.style.cssText = `
                    position: fixed;
                    bottom: 30px;
                    left: 50%;
                    transform: translateX(-50%);
                    background: var(--surface);
                    color: var(--text);
                    padding: 12px 24px;
                    border-radius: 25px;
                    font-size: 0.9rem;
                    font-weight: 600;
                    z-index: 200;
                    border: 1px solid var(--border);
                    box-shadow: 0 8px 30px rgba(0,0,0,0.4);
                    animation: fadeInUp 0.3s ease;
                    pointer-events: none;
                `;
                document.body.appendChild(toast);
            }
            toast.textContent = message;
            toast.style.display = 'block';
            toast.style.animation = 'none';
            toast.offsetHeight;
            toast.style.animation = 'fadeInUp 0.3s ease';
            clearTimeout(toast._timeout);
            toast._timeout = setTimeout(() => {
                toast.style.display = 'none';
            }, 2500);
        }

        // ==================== CHARACTER MANAGEMENT ====================
        function openCreateModal() {
            document.getElementById('modalTitle').textContent = '🌊 New Character';
            document.getElementById('charForm').reset();
            document.getElementById('editCharId').value = '';
            document.getElementById('imagePreview').style.display = 'none';
            document.getElementById('imagePlaceholder').style.display = 'flex';
            document.getElementById('modalOverlay').classList.add('active');
        }

        function openEditModal(charId) {
            const char = appData.characters.find(c => c.id === charId);
            if (!char) return;
            document.getElementById('modalTitle').textContent = '✨ Edit Character';
            document.getElementById('editCharId').value = charId;
            document.getElementById('charNameInput').value = char.name;
            document.getElementById('charRoleInput').value = char.role || '';
            document.getElementById('charPersonalityInput').value = char.personality || '';
            document.getElementById('charExampleInput').value = char.exampleDialogue || '';
            if (char.image) {
                document.getElementById('imagePreview').src = char.image;
                document.getElementById('imagePreview').style.display = 'block';
                document.getElementById('imagePlaceholder').style.display = 'none';
            } else {
                document.getElementById('imagePreview').style.display = 'none';
                document.getElementById('imagePlaceholder').style.display = 'flex';
            }
            document.getElementById('modalOverlay').classList.add('active');
        }

        function closeModal() {
            document.getElementById('modalOverlay').classList.remove('active');
        }

        function previewImage(event) {
            const file = event.target.files[0];
            if (!file) return;
            const reader = new FileReader();
            reader.onload = function(e) {
                const img = new Image();
                img.onload = function() {
                    const canvas = document.createElement('canvas');
                    const maxSize = 200;
                    let w = img.width, h = img.height;
                    if (w > h) { if (w > maxSize) { h *= maxSize / w; w = maxSize; } }
                    else { if (h > maxSize) { w *= maxSize / h; h = maxSize; } }
                    canvas.width = w;
                    canvas.height = h;
                    canvas.getContext('2d').drawImage(img, 0, 0, w, h);
                    const resized = canvas.toDataURL('image/jpeg', 0.7);
                    document.getElementById('imagePreview').src = resized;
                    document.getElementById('imagePreview').style.display = 'block';
                    document.getElementById('imagePlaceholder').style.display = 'none';
                    document.getElementById('imagePreview').dataset.imageData = resized;
                };
                img.src = e.target.result;
            };
            reader.readAsDataURL(file);
        }

        function handleFormSubmit(event) {
            event.preventDefault();
            const editId = document.getElementById('editCharId').value;
            const existingChar = editId ? appData.characters.find(c => c.id === editId) : null;
            const imageData = document.getElementById('imagePreview').dataset.imageData || 
                              (existingChar?.image || '');
            
            const charData = {
                id: editId || Date.now().toString(36) + Math.random().toString(36).slice(2),
                name: document.getElementById('charNameInput').value.trim(),
                role: document.getElementById('charRoleInput').value.trim(),
                personality: document.getElementById('charPersonalityInput').value.trim(),
                exampleDialogue: document.getElementById('charExampleInput').value.trim(),
                image: imageData,
                messages: existingChar?.messages || [],
                createdAt: existingChar?.createdAt || Date.now()
            };

            if (editId) {
                const idx = appData.characters.findIndex(c => c.id === editId);
                if (idx >= 0) appData.characters[idx] = charData;
            } else {
                appData.characters.push(charData);
            }
            saveData();
            closeModal();
            renderCharGrid();
            if (appData.currentCharId === editId) {
                openChat(editId);
            }
            showToast(editId ? 'Character updated! 💗' : 'New character created! 🌊');
        }

        function deleteCharacter(charId) {
            if (!confirm('Delete this character and all their memories forever?')) return;
            appData.characters = appData.characters.filter(c => c.id !== charId);
            if (appData.currentCharId === charId) {
                appData.currentCharId = null;
                showScreen('charSelectScreen');
            }
            saveData();
            renderCharGrid();
            showToast('Character deleted.');
        }

        function renderCharGrid() {
            const grid = document.getElementById('charGrid');
            if (appData.characters.length === 0) {
                grid.innerHTML = `
                    <div class="empty-chars">
                        <span class="emoji">🌊</span>
                        <h3>Welcome to Sea Archives</h3>
                        <p>Create your first AI companion and<br>begin your storytelling journey 💗</p>
                    </div>`;
                return;
            }
            grid.innerHTML = appData.characters.map(c => `
                <div class="char-card" onclick="openChat('${c.id}')">
                    <button class="char-delete" onclick="event.stopPropagation(); deleteCharacter('${c.id}')">×</button>
                    <div class="char-avatar">
                        ${c.image ? `<img src="${c.image}" alt="${escapeHTML(c.name)}">` : escapeHTML(c.name.charAt(0).toUpperCase())}
                    </div>
                    <div class="char-name">${escapeHTML(c.name)}</div>
                    <div class="char-role">${escapeHTML(c.role || 'Mysterious Soul')}</div>
                    <div class="char-messages-badge">💬 ${c.messages.length} memories</div>
                </div>
            `).join('');
        }

        // ==================== CHAT ====================
        function openChat(charId) {
            appData.currentCharId = charId;
            const char = appData.characters.find(c => c.id === charId);
            if (!char) return;
            
            document.getElementById('chatCharName').textContent = char.name;
            const avatarEl = document.getElementById('chatCharAvatar');
            if (char.image) {
                avatarEl.innerHTML = `<img src="${char.image}" alt="${escapeHTML(char.name)}" style="width:100%;height:100%;border-radius:50%;object-fit:cover;">`;
            } else {
                avatarEl.textContent = char.name.charAt(0).toUpperCase();
            }
            document.getElementById('chatCharStatus').textContent = char.personality ? '💗 Memories intact' : '🌊 Connected';
            
            renderMessages();
            showScreen('chatScreen');
            scrollToBottom();
            document.getElementById('messageInput').focus();
        }

        function goBack() {
            appData.currentCharId = null;
            showScreen('charSelectScreen');
            renderCharGrid();
        }

        function editCurrentChar() {
            if (appData.currentCharId) openEditModal(appData.currentCharId);
        }

        function clearCurrentChat() {
            if (!appData.currentCharId) return;
            if (!confirm('Clear all memories with this character?')) return;
            const char = appData.characters.find(c => c.id === appData.currentCharId);
            if (char) {
                char.messages = [];
                saveData();
                renderMessages();
                showToast('Memories cleared. A fresh start.');
            }
        }

        function renderMessages() {
            const char = appData.characters.find(c => c.id === appData.currentCharId);
            const container = document.getElementById('chatMessages');
            const typingEl = document.getElementById('typingIndicator');
            
            container.innerHTML = '';
            container.appendChild(typingEl);
            
            if (!char || char.messages.length === 0) {
                const welcome = document.createElement('div');
                welcome.className = 'message ai';
                const avatarContent = char?.image 
                    ? `<img src="${char.image}" alt="">` 
                    : (char?.name?.charAt(0) || '🌊');
                welcome.innerHTML = `
                    <div class="message-avatar">${avatarContent}</div>
                    <div>
                        <div class="message-bubble">${char?.personality 
                            ? `*${char.name} looks at you with knowing eyes.* Welcome to my world. I remember everything we share here. Shall we begin our story? 💗`
                            : `Hello! I'm ${char?.name || 'here'}. What story shall we tell together? 🌊`}</div>
                        <div class="timestamp">now</div>
                    </div>`;
                container.insertBefore(welcome, typingEl);
                return;
            }
            
            char.messages.forEach(msg => {
                const div = document.createElement('div');
                div.className = `message ${msg.role}`;
                const avatarContent = msg.role === 'user' 
                    ? '👤'
                    : (char.image ? `<img src="${char.image}" alt="">` : escapeHTML(char.name.charAt(0)));
                div.innerHTML = `
                    <div class="message-avatar">${avatarContent}</div>
                    <div>
                        <div class="message-bubble">${escapeHTML(msg.content)}</div>
                        <div class="timestamp">${formatTime(msg.timestamp)}</div>
                    </div>`;
                container.insertBefore(div, typingEl);
            });
        }

        async function sendMessage() {
            const input = document.getElementById('messageInput');
            const text = input.value.trim();
            if (!text || !appData.currentCharId) return;
            
            if (!appData.apiKey) {
                showToast('⚠️ Please enter your Groq API key first!');
                return;
            }

            const char = appData.characters.find(c => c.id === appData.currentCharId);
            if (!char) return;

            char.messages.push({
                role: 'user',
                content: text,
                timestamp: Date.now()
            });
            saveData();
            renderMessages();
            scrollToBottom();
            input.value = '';
            input.style.height = 'auto';

            const typingEl = document.getElementById('typingIndicator');
            typingEl.classList.add('active');
            document.getElementById('sendBtn').disabled = true;
            scrollToBottom();

            try {
                const response = await callGroqAPI(char);
                char.messages.push({
                    role: 'assistant',
                    content: response,
                    timestamp: Date.now()
                });
                saveData();
                renderMessages();
            } catch (error) {
                console.error('API Error:', error);
                char.messages.push({
                    role: 'assistant',
                    content: error.message || '*The waves are rough... I couldn\'t respond. Check your API key?*',
                    timestamp: Date.now()
                });
                saveData();
                renderMessages();
            } finally {
                typingEl.classList.remove('active');
                document.getElementById('sendBtn').disabled = false;
                scrollToBottom();
                input.focus();
            }
        }

        async function callGroqAPI(char) {
            let systemPrompt = `You are ${char.name}`;
            if (char.role) systemPrompt += `, ${char.role}`;
            systemPrompt += `. You are roleplaying in a story-driven chat. Stay completely in character.\n\n`;
            
            if (char.personality) {
                systemPrompt += `📜 YOUR PERSONALITY & BACKSTORY:\n${char.personality}\n\n`;
            }
            if (char.exampleDialogue) {
                systemPrompt += `💬 EXAMPLE OF YOUR VOICE:\n${char.exampleDialogue}\n\n`;
            }
            systemPrompt += `🌊 SACRED RULES:
- Remember everything from the conversation history. Reference past moments naturally.
- Never break character or mention being an AI. You ARE ${char.name}.
- Respond like a real person: 1-3 paragraphs, engaging and natural.
- For storytelling: collaborate enthusiastically, add vivid details, ask questions, advance the plot.
- Adapt your tone organically — be playful, mysterious, tender, or bold as your character would.`;

            const apiMessages = [
                { role: 'system', content: systemPrompt }
            ];
            
            const recentMessages = char.messages.slice(-30);
            recentMessages.forEach(msg => {
                apiMessages.push({
                    role: msg.role === 'user' ? 'user' : 'assistant',
                    content: msg.content
                });
            });

            const response = await fetch('https://api.groq.com/openai/v1/chat/completions', {
                method: 'POST',
                headers: {
                    'Authorization': `Bearer ${appData.apiKey}`,
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({
                    model: 'llama-3.3-70b-versatile',
                    messages: apiMessages,
                    temperature: 0.9,
                    max_tokens: 500,
                    top_p: 0.95
                })
            });

            if (!response.ok) {
                const err = await response.json().catch(() => ({}));
                throw new Error(err.error?.message || `The tides are rough (Error ${response.status})`);
            }

            const data = await response.json();
            return data.choices[0].message.content;
        }

        // ==================== HELPERS ====================
        function showScreen(screenId) {
            document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
            document.getElementById(screenId).classList.add('active');
        }

        function scrollToBottom() {
            setTimeout(() => {
                const container = document.getElementById('chatMessages');
                container.scrollTop = container.scrollHeight;
            }, 100);
        }

        function formatTime(timestamp) {
            const d = new Date(timestamp);
            return d.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
        }

        function escapeHTML(str) {
            const div = document.createElement('div');
            div.textContent = str;
            return div.innerHTML;
        }

        function handleKeyDown(event) {
            if (event.key === 'Enter' && !event.shiftKey) {
                event.preventDefault();
                sendMessage();
            }
        }

        document.addEventListener('DOMContentLoaded', () => {
            const textarea = document.getElementById('messageInput');
            textarea.addEventListener('input', () => {
                textarea.style.height = 'auto';
                textarea.style.height = Math.min(textarea.scrollHeight, 120) + 'px';
            });
            
            document.getElementById('modalOverlay').addEventListener('click', function(e) {
                if (e.target === this) closeModal();
            });

            loadData();
            renderCharGrid();
        });
    </script>
</body>
</html>