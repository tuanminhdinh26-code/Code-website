<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>EthosAI - Digital Empathy & Ethics Training</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #6366f1;
            --primary-light: #818cf8;
            --secondary: #ec4899;
            --bg-gradient: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            --glass-bg: rgba(255, 255, 255, 0.85);
            --glass-border: rgba(255, 255, 255, 0.5);
            --text-main: #1e293b;
            --text-muted: #64748b;
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #ef4444;
            --radius: 16px;
            --shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Inter', sans-serif;
        }

        body {
            background: var(--bg-gradient);
            min-height: 100vh;
            color: var(--text-main);
            overflow-x: hidden;
        }

        /* --- Layout & Nav --- */
        .app-container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
            display: flex;
            flex-direction: column;
            min-height: 100vh;
        }

        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px 0;
            margin-bottom: 20px;
        }

        .logo {
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--primary);
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .nav-links {
            display: flex;
            gap: 20px;
        }

        .nav-btn {
            background: transparent;
            border: none;
            color: var(--text-muted);
            font-weight: 500;
            cursor: pointer;
            padding: 8px 16px;
            border-radius: 8px;
            transition: all 0.3s ease;
        }

        .nav-btn:hover, .nav-btn.active {
            background: white;
            color: var(--primary);
            box-shadow: 0 2px 5px rgba(0,0,0,0.05);
        }

        /* --- Page Management --- */
        .page {
            display: none;
            animation: fadeIn 0.5s ease;
        }

        .page.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* --- Components --- */
        .card {
            background: var(--glass-bg);
            backdrop-filter: blur(10px);
            border: 1px solid var(--glass-border);
            border-radius: var(--radius);
            padding: 24px;
            box-shadow: var(--shadow);
            margin-bottom: 20px;
        }

        .btn-primary {
            background: var(--primary);
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: var(--radius);
            font-weight: 600;
            cursor: pointer;
            transition: transform 0.2s, box-shadow 0.2s;
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(99, 102, 241, 0.3);
        }

        /* --- Home Page --- */
        .hero {
            text-align: center;
            padding: 60px 20px;
        }

        .hero h1 {
            font-size: 3rem;
            margin-bottom: 20px;
            background: linear-gradient(to right, var(--primary), var(--secondary));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .hero p {
            font-size: 1.2rem;
            color: var(--text-muted);
            max-width: 600px;
            margin: 0 auto 40px;
        }

        .features-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 40px;
        }

        .feature-card {
            text-align: center;
            padding: 30px;
        }

        .feature-icon {
            font-size: 2rem;
            margin-bottom: 15px;
            display: block;
        }

        .companion-section {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 40px;
            margin-top: 60px;
            flex-wrap: wrap;
        }

        .companion-img {
            width: 300px;
            height: 300px;
            border-radius: 50%;
            object-fit: cover;
            border: 4px solid white;
            box-shadow: var(--shadow);
        }

        /* --- Chat Page --- */
        .chat-container {
            display: grid;
            grid-template-columns: 1fr 350px;
            gap: 20px;
            height: calc(100vh - 150px);
        }

        .chat-main {
            display: flex;
            flex-direction: column;
        }

        .chat-history {
            flex: 1;
            overflow-y: auto;
            padding: 20px;
            background: rgba(255,255,255,0.4);
            border-radius: var(--radius);
            margin-bottom: 20px;
        }

        .message {
            margin-bottom: 15px;
            max-width: 80%;
            padding: 15px;
            border-radius: 12px;
            line-height: 1.5;
        }

        .message.user {
            background: var(--primary);
            color: white;
            margin-left: auto;
            border-bottom-right-radius: 2px;
        }

        .message.ai {
            background: white;
            color: var(--text-main);
            border: 1px solid #e2e8f0;
            border-bottom-left-radius: 2px;
        }

        .input-area {
            display: flex;
            gap: 10px;
        }

        .chat-input {
            flex: 1;
            padding: 15px;
            border: 1px solid #e2e8f0;
            border-radius: var(--radius);
            outline: none;
            font-size: 1rem;
        }

        .analysis-panel {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        .score-box {
            background: white;
            padding: 15px;
            border-radius: 12px;
            border-left: 5px solid var(--primary);
        }

        .score-label {
            font-size: 0.85rem;
            color: var(--text-muted);
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .score-value {
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--text-main);
        }

        .risk-badge {
            display: inline-block;
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 600;
            color: white;
            margin-top: 5px;
        }

        /* --- Voice Page --- */
        .voice-container {
            max-width: 600px;
            margin: 40px auto;
            text-align: center;
        }

        .mic-button {
            width: 120px;
            height: 120px;
            border-radius: 50%;
            background: white;
            border: none;
            box-shadow: 0 0 0 0 rgba(236, 72, 153, 0.7);
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 30px;
            transition: all 0.3s;
        }

        .mic-button:hover {
            transform: scale(1.05);
        }

        .mic-button.recording {
            animation: pulse 1.5s infinite;
            background: var(--secondary);
        }

        .mic-button svg {
            width: 40px;
            height: 40px;
            fill: var(--secondary);
        }

        .mic-button.recording svg {
            fill: white;
        }

        @keyframes pulse {
            0% { box-shadow: 0 0 0 0 rgba(236, 72, 153, 0.7); }
            70% { box-shadow: 0 0 0 30px rgba(236, 72, 153, 0); }
            100% { box-shadow: 0 0 0 0 rgba(236, 72, 153, 0); }
        }

        .waveform {
            height: 60px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 5px;
            margin-bottom: 20px;
        }

        .bar {
            width: 6px;
            background: var(--primary);
            border-radius: 3px;
            height: 10px;
            transition: height 0.1s;
        }

        .recording .bar {
            animation: wave 0.5s infinite ease-in-out;
        }

        @keyframes wave {
            0%, 100% { height: 10px; }
            50% { height: 40px; }
        }

        /* --- Story Page --- */
        .story-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 25px;
        }

        .story-card {
            cursor: pointer;
            transition: transform 0.3s;
            overflow: hidden;
            position: relative;
        }

        .story-card:hover {
            transform: translateY(-5px);
        }

        .story-card img {
            width: 100%;
            height: 180px;
            object-fit: cover;
        }

        .story-content {
            padding: 20px;
        }

        .story-tag {
            font-size: 0.75rem;
            background: #e0e7ff;
            color: var(--primary);
            padding: 4px 8px;
            border-radius: 4px;
            text-transform: uppercase;
            font-weight: 600;
        }

        /* --- Dashboard --- */
        .dashboard-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 20px;
        }

        .stat-card {
            background: white;
            padding: 20px;
            border-radius: var(--radius);
            text-align: center;
        }

        .stat-number {
            font-size: 2.5rem;
            font-weight: 700;
            color: var(--primary);
        }

        /* --- Modal --- */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            opacity: 0;
            transition: opacity 0.3s;
        }

        .modal-overlay.open {
            display: flex;
            opacity: 1;
        }

        .modal-content {
            background: white;
            padding: 30px;
            border-radius: var(--radius);
            max-width: 500px;
            width: 90%;
            position: relative;
            transform: scale(0.9);
            transition: transform 0.3s;
        }

        .modal-overlay.open .modal-content {
            transform: scale(1);
        }

        .close-modal {
            position: absolute;
            top: 15px;
            right: 15px;
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
        }

        /* --- Responsive --- */
        @media (max-width: 768px) {
            .chat-container {
                grid-template-columns: 1fr;
                height: auto;
            }
            .analysis-panel {
                margin-top: 20px;
            }
            .dashboard-grid {
                grid-template-columns: 1fr;
            }
            .nav-links {
                display: none; /* Simplify for mobile demo */
            }
            .companion-section {
                flex-direction: column-reverse;
            }
        }
    </style>
</head>
<body>

<div class="app-container">
    <nav>
        <div class="logo">
            <svg width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 2a10 10 0 1 0 10 10H12V2z"></path><path d="M12 12 2.1 12.1"></path><path d="M12 12 19.3 4.7"></path></svg>
            EthosAI
        </div>
        <div class="nav-links">
            <button class="nav-btn active" onclick="showPage('home')">Home</button>
            <button class="nav-btn" onclick="showPage('chat')">Chat Training</button>
            <button class="nav-btn" onclick="showPage('voice')">Voice Mode</button>
            <button class="nav-btn" onclick="showPage('story')">Stories</button>
            <button class="nav-btn" onclick="showPage('dashboard')">Dashboard</button>
        </div>
    </nav>

    <!-- HOME PAGE -->
    <div id="home" class="page active">
        <div class="hero">
            <h1>Master Digital Empathy & Ethics</h1>
            <p>An AI-powered companion to help you navigate online conflicts, improve emotional intelligence, and communicate with respect.</p>
            <button class="btn-primary" onclick="showPage('chat')">Start Training</button>
        </div>

        <div class="features-grid">
            <div class="card feature-card">
                <span class="feature-icon">🧠</span>
                <h3>AI Analysis</h3>
                <p>Real-time feedback on your sentiment and moral alignment.</p>
            </div>
            <div class="card feature-card">
                <span class="feature-icon">🎙️</span>
                <h3>Voice Mode</h3>
                <p>Practice tone and inflection with speech-to-text integration.</p>
            </div>
            <div class="card feature-card">
                <span class="feature-icon">📚</span>
                <h3>Story Scenarios</h3>
                <p>Interactive scenarios about cyberbullying and conflict.</p>
            </div>
        </div>

        <div class="companion-section">
            <div>
                <h2>Meet Aura, Your Guide</h2>
                <p style="margin: 20px 0; color: var(--text-muted);">Aura is a Live2D companion designed to help you reflect on your digital interactions. She provides gentle nudges and celebrates your progress in emotional regulation.</p>
                <button class="btn-primary" onclick="showPage('chat')">Chat with Aura</button>
            </div>
            <img src="https://image.pollinations.ai/prompt/cute%20friendly%203d%20robot%20girl%20companion%20character%20blue%20and%20white%20color%20scheme%20educational%20style%20soft%20lighting?width=400&height=400&nologo=true" alt="AI Companion Aura" class="companion-img">
        </div>
    </div>

    <!-- CHAT PAGE -->
    <div id="chat" class="page">
        <div class="chat-container">
            <div class="chat-main card">
                <div class="chat-history" id="chatHistory">
                    <div class="message ai">
                        Hello! I'm Aura. Tell me about a situation that's bothering you, or practice a difficult conversation. I'll help you analyze it.
                    </div>
                </div>
                <div class="input-area">
                    <input type="text" id="chatInput" class="chat-input" placeholder="Type your message here..." onkeypress="handleEnter(event)">
                    <button class="btn-primary" onclick="sendMessage()">Send</button>
                </div>
            </div>
            
            <div class="analysis-panel" id="analysisPanel">
                <div class="card score-box" style="border-left-color: var(--primary);">
                    <div class="score-label">Emotion Detected</div>
                    <div class="score-value" id="scoreEmotion">-</div>
                </div>
                <div class="card score-box" style="border-left-color: #8b5cf6;">
                    <div class="score-label">Sentiment Score</div>
                    <div class="score-value" id="scoreSentiment">-</div>
                </div>
                <div class="card score-box" style="border-left-color: #06b6d4;">
                    <div class="score-label">Communication</div>
                    <div class="score-value" id="scoreComm">-</div>
                </div>
                <div class="card score-box" style="border-left-color: #f43f5e;">
                    <div class="score-label">Moral Alignment</div>
                    <div class="score-value" id="scoreMoral">-</div>
                </div>
                <div class="card score-box" style="border-left-color: #64748b;">
                    <div class="score-label">Risk Level</div>
                    <div id="scoreRisk" class="risk-badge" style="background: #cbd5e1;">-</div>
                </div>
                
                <div class="card" style="background: #f0fdf4; border: 1px solid #bbf7d0;">
                    <h4 style="color: #166534; margin-bottom: 10px;">💡 Improved Expression</h4>
                    <p id="feedbackExpression" style="font-size: 0.9rem; color: #14532d;">Waiting for input...</p>
                </div>
                
                <div class="card" style="background: #fff7ed; border: 1px solid #fed7aa;">
                    <h4 style="color: #9a3412; margin-bottom: 10px;">🎓 Educational Feedback</h4>
                    <p id="feedbackEdu" style="font-size: 0.9rem; color: #7c2d12;">Waiting for input...</p>
                </div>
            </div>
        </div>
    </div>

    <!-- VOICE PAGE -->
    <div id="voice" class="page">
        <div class="voice-container card">
            <h2 style="margin-bottom: 20px;">Voice Practice Mode</h2>
            <button class="mic-button" id="micBtn" onclick="toggleRecording()">
                <svg viewBox="0 0 24 24"><path d="M12 1a3 3 0 0 0-3 3v8a3 3 0 0 0 6 0V4a3 3 0 0 0-3-3z"></path><path d="M19 10v2a7 7 0 0 1-14 0v-2"></path><line x1="12" y1="19" x2="12" y2="23"></line><line x1="8" y1="23" x2="16" y2="23"></line></svg>
            </button>
            <div class="waveform" id="waveform">
                <div class="bar"></div><div class="bar"></div><div class="bar"></div>
                <div class="bar"></div><div class="bar"></div><div class="bar"></div>
                <div class="bar"></div><div class="bar"></div><div class="bar"></div>
                <div class="bar"></div><div class="bar"></div><div class="bar"></div>
            </div>
            <div id="transcriptArea" style="min-height: 100px; margin-bottom: 20px; color: var(--text-muted); font-style: italic;">
                Press the microphone to start speaking...
            </div>
            <div id="voiceResults" style="display: none; text-align: left;">
                <h4>Analysis Results:</h4>
                <p><strong>Tone:</strong> <span id="voiceTone">-</span></p>
                <p><strong>Clarity:</strong> <span id="voiceClarity">-</span></p>
                <p><strong>Empathy Level:</strong> <span id="voiceEmpathy">-</span></p>
            </div>
        </div>
    </div>

    <!-- STORY PAGE -->
    <div id="story" class="page">
        <h2 style="margin-bottom: 20px;">Ethical Scenarios</h2>
        <div class="story-grid" id="storyGrid">
            <!-- Cards injected by JS -->
        </div>
    </div>

    <!-- DASHBOARD PAGE -->
    <div id="dashboard" class="page">
        <h2 style="margin-bottom: 20px;">Your Progress</h2>
        <div class="dashboard-grid">
            <div class="stat-card">
                <div class="stat-number" id="totalSessions">12</div>
                <div>Total Sessions</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" id="avgScore">8.4</div>
                <div>Avg. Communication Score</div>
            </div>
        </div>
        
        <div class="card" style="margin-top: 20px;">
            <canvas id="progressChart"></canvas>
        </div>
        
        <div class="card" style="margin-top: 20px;">
            <canvas id="emotionChart"></canvas>
        </div>
    </div>

</div>

<!-- STORY MODAL -->
<div class="modal-overlay" id="storyModal">
    <div class="modal-content">
        <button class="close-modal" onclick="closeModal()">&times;</button>
        <h2 id="modalTitle" style="margin-bottom: 15px;">Title</h2>
        <p id="modalSituation" style="margin-bottom: 20px; line-height: 1.6;">Situation...</p>
        <div style="background: #f0f9ff; padding: 15px; border-radius: 8px; border-left: 4px solid var(--primary);">
            <strong>Moral Lesson:</strong>
            <p id="modalLesson" style="margin-top: 5px;">Lesson...</p>
        </div>
    </div>
</div>

<script>
    // --- Navigation ---
    function showPage(pageId) {
        document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
        document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
        
        document.getElementById(pageId).classList.add('active');
        
        // Highlight nav button
        const navBtns = document.querySelectorAll('.nav-btn');
        if(pageId === 'home') navBtns[0].classList.add('active');
        if(pageId === 'chat') navBtns[1].classList.add('active');
        if(pageId === 'voice') navBtns[2].classList.add('active');
        if(pageId === 'story') navBtns[3].classList.add('active');
        if(pageId === 'dashboard') {
            navBtns[4].classList.add('active');
            initCharts();
        }
    }

    // --- Chat Logic ---
    function handleEnter(e) {
        if(e.key === 'Enter') sendMessage();
    }

    async function sendMessage() {
        const input = document.getElementById('chatInput');
        const history = document.getElementById('chatHistory');
        const text = input.value.trim();
        
        if(!text) return;

        // User Message
        const userMsg = document.createElement('div');
        userMsg.className = 'message user';
        userMsg.textContent = text;
        history.appendChild(userMsg);
        
        input.value = '';
        history.scrollTop = history.scrollHeight;

        // Loading State
        const loadingMsg = document.createElement('div');
        loadingMsg.className = 'message ai';
        loadingMsg.textContent = 'Analyzing sentiment and ethics...';
        loadingMsg.id = 'loadingMsg';
        history.appendChild(loadingMsg);
        history.scrollTop = history.scrollHeight;

        // Mock API Call
        try {
            const response = await mockApiCall(text);
            
            // Remove loading
            document.getElementById('loadingMsg').remove();

            // AI Response
            const aiMsg = document.createElement('div');
            aiMsg.className = 'message ai';
            aiMsg.textContent = response.educational_feedback;
            history.appendChild(aiMsg);
            history.scrollTop = history.scrollHeight;

            // Update Dashboard
            updateAnalysisPanel(response);

        } catch (error) {
            console.error(error);
        }
    }

    function updateAnalysisPanel(data) {
        // Scores
        document.getElementById('scoreEmotion').textContent = data.emotion_type;
        document.getElementById('scoreSentiment').textContent = data.sentiment_score.toFixed(1);
        document.getElementById('scoreComm').textContent = data.communication_score + '/10';
        document.getElementById('scoreMoral').textContent = data.moral_alignment_score + '/10';
        
        const riskBadge = document.getElementById('scoreRisk');
        riskBadge.textContent = data.risk_level.toUpperCase();
        
        // Dynamic Styling based on Risk
        let riskColor = '#cbd5e1'; // default gray
        let panelColor = 'var(--primary)';

        if(data.risk_level === 'low') {
            riskColor = 'var(--success)';
            panelColor = 'var(--success)';
        } else if (data.risk_level === 'medium') {
            riskColor = 'var(--warning)';
            panelColor = 'var(--warning)';
        } else if (data.risk_level === 'high') {
            riskColor = 'var(--danger)';
            panelColor = 'var(--danger)';
        }

        riskBadge.style.backgroundColor = riskColor;
        document.querySelector('.analysis-panel').style.borderLeft = `5px solid ${panelColor}`;

        // Feedback Text
        document.getElementById('feedbackExpression').textContent = data.recommended_expression;
        document.getElementById('feedbackEdu').textContent = `Topic: ${data.moral_lesson_topic}. ${data.educational_feedback}`;
    }

    // Mock API Function
    function mockApiCall(text) {
        return new Promise(resolve => {
            setTimeout(() => {
                // Simple heuristic for demo purposes
                const lowerText = text.toLowerCase();
                let risk = 'low';
                let emotion = 'Neutral';
                let commScore = 8;
                let moralScore = 9;
                let feedback = "That sounds like a reasonable perspective. Try to maintain this tone.";
                let expression = "I understand your point, however...";
                let topic = "Respectful Dialogue";

                if(lowerText.includes('hate') || lowerText.includes('stupid') || lowerText.includes('kill')) {
                    risk = 'high';
                    emotion = 'Anger';
                    commScore = 2;
                    moralScore = 1;
                    feedback = "This language is harmful and violates digital ethics. It can cause real emotional damage.";
                    expression = "I feel frustrated because...";
                    topic = "Hate Speech & Harm";
                } else if (lowerText.includes('sad') || lowerText.includes('cry') || lowerText.includes('lonely')) {
                    risk = 'medium';
                    emotion = 'Sadness';
                    commScore = 6;
                    moralScore = 8;
                    feedback = "It's okay to feel this way. Consider reaching out to a trusted friend or adult.";
                    expression = "I'm feeling down and could use some support.";
                    topic = "Emotional Vulnerability";
                } else if (lowerText.includes('disagree') || lowerText.includes('wrong')) {
                    risk = 'low';
                    emotion = 'Assertive';
                    commScore = 9;
                    moralScore = 9;
                    feedback = "Good job expressing disagreement without being aggressive.";
                    expression = "I see it differently because...";
                    topic = "Constructive Disagreement";
                }

                resolve({
                    emotion_type: emotion,
                    sentiment_score: risk === 'high' ? -0.8 : (risk === 'medium' ? -0.2 : 0.6),
                    communication_score: commScore,
                    moral_alignment_score: moralScore,
                    risk_level: risk,
                    educational_feedback: feedback,
                    recommended_expression: expression,
                    moral_lesson_topic: topic
                });
            }, 1000);
        });
    }

    // --- Voice Logic ---
    let isRecording = false;
    function toggleRecording() {
        const btn = document.getElementById('micBtn');
        const waveform = document.getElementById('waveform');
        const transcript = document.getElementById('transcriptArea');
        const results = document.getElementById('voiceResults');

        isRecording = !isRecording;

        if(isRecording) {
            btn.classList.add('recording');
            waveform.classList.add('recording');
            transcript.textContent = "Listening...";
            results.style.display = 'none';
            
            // Simulate recording duration
            setTimeout(() => {
                if(isRecording) toggleRecording(); // Auto stop after 3s for demo
            }, 3000);
        } else {
            btn.classList.remove('recording');
            waveform.classList.remove('recording');
            transcript.textContent = "Transcript: 'I think we should listen to both sides before deciding.'";
            
            // Show mock results
            results.style.display = 'block';
            document.getElementById('voiceTone').textContent = "Calm & Measured";
            document.getElementById('voiceClarity').textContent = "95%";
            document.getElementById('voiceEmpathy').textContent = "High";
        }
    }

    // --- Story Logic ---
    const stories = [
        {
            title: "The Group Chat Exclusion",
            category: "Cyberbullying",
            situation: "You notice your friends created a group chat without you, and they are posting screenshots of inside jokes you don't understand.",
            lesson: "Exclusion can be as hurtful as direct insults. It's important to communicate feelings of loneliness rather than reacting with anger."
        },
        {
            title: "The Misunderstood Sarcasm",
            category: "Misunderstanding",
            situation: "You made a joke in a public comment section, but someone took it seriously and called you out aggressively.",
            lesson: "Text lacks tone. When conflicts arise online, assume positive intent first and clarify your meaning calmly."
        },
        {
            title: "Exam Stress Venting",
            category: "Academic Stress",
            situation: "You are overwhelmed with finals and tempted to post a rant about how 'useless' the teachers are.",
            lesson: "Venting is natural, but public shaming damages relationships. Seek private support channels instead."
        },
        {
            title: "Friendship Conflict",
            category: "Friendship",
            situation: "Your best friend posted a photo with someone you had a fight with last week.",
            lesson: "Social media highlights can be misleading. Address conflicts directly with friends rather than guessing through posts."
        }
    ];

    function renderStories() {
        const grid = document.getElementById('storyGrid');
        grid.innerHTML = stories.map((story, index) => `
            <div class="card story-card" onclick="openModal(${index})">
                <img src="https://image.pollinations.ai/prompt/illustration%20of%20${story.category.replace(' ', '%20')}%20scenario%20digital%20art%20soft%20colors?width=400&height=200&nologo=true" alt="${story.category}">
                <div class="story-content">
                    <span class="story-tag">${story.category}</span>
                    <h3 style="margin-top: 10px;">${story.title}</h3>
                </div>
            </div>
        `).join('');
    }

    function openModal(index) {
        const story = stories[index];
        document.getElementById('modalTitle').textContent = story.title;
        document.getElementById('modalSituation').textContent = story.situation;
        document.getElementById('modalLesson').textContent = story.lesson;
        document.getElementById('storyModal').classList.add('open');
    }

    function closeModal() {
        document.getElementById('storyModal').classList.remove('open');
    }

    // Close modal on outside click
    document.getElementById('storyModal').addEventListener('click', (e) => {
        if(e.target === document.getElementById('storyModal')) closeModal();
    });

    // --- Dashboard Charts ---
    let progressChartInstance = null;
    let emotionChartInstance = null;

    function initCharts() {
        const ctxProgress = document.getElementById('progressChart').getContext('2d');
        const ctxEmotion = document.getElementById('emotionChart').getContext('2d');

        if(progressChartInstance) progressChartInstance.destroy();
        if(emotionChartInstance) emotionChartInstance.destroy();

        // Line Chart
        progressChartInstance = new Chart(ctxProgress, {
            type: 'line',
            data: {
                labels: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
                datasets: [{
                    label: 'Communication Score',
                    data: [6.5, 7.0, 6.8, 8.2, 8.5, 9.0, 8.8],
                    borderColor: '#6366f1',
                    tension: 0.4,
                    fill: true,
                    backgroundColor: 'rgba(99, 102, 241, 0.1)'
                }]
            },
            options: {
                responsive: true,
                plugins: {
                    legend: { display: false },
                    title: { display: true, text: 'Weekly Progress' }
                }
            }
        });

        // Bar Chart
        emotionChartInstance = new Chart(ctxEmotion, {
            type: 'bar',
            data: {
                labels: ['Joy', 'Sadness', 'Anger', 'Fear', 'Surprise'],
                datasets: [{
                    label: 'Emotion Frequency',
                    data: [12, 5, 3, 2, 4],
                    backgroundColor: [
                        '#10b981', '#3b82f6', '#ef4444', '#f59e0b', '#8b5cf6'
                    ],
                    borderRadius: 5
                }]
            },
            options: {
                responsive: true,
                plugins: {
                    legend: { display: false },
                    title: { display: true, text: 'Emotional Distribution' }
                },
                scales: {
                    y: { beginAtZero: true }
                }
            }
        });
    }

    // Initialize
    renderStories();

</script>
</body>
</html>

