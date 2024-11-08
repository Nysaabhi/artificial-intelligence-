<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Deep Chatbot</title>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
:root {
    --primary-color: #FFD700;
    --secondary-color: #FDB931;
    --background-dark: #1a1a1f;
    --text-light: #ffffff;
    --text-dark: #000000;
    --accent-gradient: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
}

* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    font-family: 'Poppins', sans-serif;
    background-color: var(--background-dark);
    color: var(--text-light);
    line-height: 1.6;
    min-height: 100vh;
    overflow-x: hidden;
}

/* Header Styles */
.header {
    padding: 8px 16px;
    background: rgba(26, 26, 31, 0.95);
    position: fixed;
    width: 100%;
    top: 0;
    left: 0;
    z-index: 1000;
    border-bottom: 2px solid var(--primary-color);
    backdrop-filter: blur(10px);
    height: 60px;
}

.header-content {
    max-width: 1400px;
    margin: 0 auto;
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 100%;
}

.logo {
    font-size: 1.8em;
    font-weight: 900;
    background: var(--accent-gradient);
    -webkit-background-clip: text;
    color: transparent;
    letter-spacing: 1.2px;
}

.connect-wallet {
    padding: 10px 20px;
    background: var(--accent-gradient);
    border: none;
    border-radius: 50px;
    color: var(--text-dark);
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s ease;
    font-size: 0.95em;
    letter-spacing: 0.5px;
}

.connect-wallet:hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(255, 215, 0, 0.2);
}

/* Chatbot Container */
.chatbot-container {
    position: fixed;
    top: 60px;
    left: 0;
    right: 0;
    height: calc(100vh - 60px);
    background: rgba(26, 26, 31, 0.95);
    display: flex;
    flex-direction: column;
    z-index: 999;
    backdrop-filter: blur(10px);
    border: 1px solid rgba(255, 215, 0, 0.1);
}

/* Chat Header */
.chat-header {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 60px;
    padding: 15px;
    background: linear-gradient(135deg, rgba(255, 215, 0, 0.1), rgba(253, 185, 49, 0.1));
    border-bottom: 1px solid rgba(255, 215, 0, 0.2);
    display: flex;
    justify-content: space-between;
    align-items: center;
    z-index: 2;
}

.chat-status {
    display: flex;
    align-items: center;
    color: var(--primary-color);
    font-weight: 600;
    font-size: 0.95em;
}

.status-dot {
    width: 8px;
    height: 8px;
    background: var(--primary-color);
    border-radius: 50%;
    margin-right: 8px;
    animation: pulse 2s infinite;
}

/* Chat Messages */
.chat-messages {
    position: absolute;
    top: 60px;
    bottom: 70px;
    left: 0;
    right: 0;
    overflow-y: auto;
    padding: 20px;
    display: flex;
    flex-direction: column;
    gap: 16px;
    scrollbar-width: thin;
    scrollbar-color: var(--primary-color) transparent;
}

.chat-messages::-webkit-scrollbar {
    width: 6px;
}

.chat-messages::-webkit-scrollbar-track {
    background: transparent;
}

.chat-messages::-webkit-scrollbar-thumb {
    background-color: var(--primary-color);
    border-radius: 3px;
}

.message {
    display: flex;
    gap: 12px;
    max-width: 85%;
    animation: messageSlide 0.3s ease-out;
}

.bot-message {
    align-self: flex-start;
}

.user-message {
    align-self: flex-end;
    flex-direction: row-reverse;
}

.message-avatar {
    width: 36px;
    height: 36px;
    background: rgba(255, 215, 0, 0.1);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    color: var(--primary-color);
}

.message-content {
    background: rgba(255, 255, 255, 0.05);
    padding: 12px 16px;
    border-radius: 16px;
    color: var(--text-light);
    font-size: 0.95em;
}

.user-message .message-content {
    background: rgba(255, 215, 0, 0.1);
}

/* Chat Input */
.chat-input-container {
    position: fixed;
    bottom: 60px;
    left: 0;
    right: 0;
    height: 70px;
    padding: 16px;
    border-top: 1px solid rgba(255, 215, 0, 0.1);
    display: flex;
    gap: 12px;
    align-items: center;
    background: rgba(26, 26, 31, 0.95);
    z-index: 2;
}

#chatInput {
    flex: 1;
    background: rgba(255, 255, 255, 0.05);
    border: 1px solid rgba(255, 215, 0, 0.2);
    border-radius: 12px;
    padding: 12px 16px;
    color: var(--text-light);
    font-size: 0.95em;
    transition: all 0.3s ease;
}

#chatInput:focus {
    outline: none;
    border-color: var(--primary-color);
    background: rgba(255, 255, 255, 0.08);
}

.input-actions {
    display: flex;
    gap: 8px;
}

.input-actions button {
    background: none;
    border: none;
    color: rgba(255, 215, 0, 0.7);
    cursor: pointer;
    padding: 8px;
    border-radius: 50%;
    transition: all 0.3s ease;
    display: flex;
    align-items: center;
    justify-content: center;
}

.input-actions button:hover {
    color: var(--primary-color);
    background: rgba(255, 215, 0, 0.1);
}

/* Bottom Navigation */
.bottom-nav {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    background: rgba(26, 26, 31, 0.95);
    padding: 8px 0;
    backdrop-filter: blur(10px);
    border-top: 1px solid rgba(255, 215, 0, 0.2);
    z-index: 1000;
    height: 60px;
}

.nav-container {
    display: flex;
    justify-content: space-around;
    align-items: center;
    max-width: 600px;
    margin: 0 auto;
    height: 100%;
}

.nav-item {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-decoration: none;
    color: #fff;
    transition: all 0.3s ease;
    padding: 5px;
    cursor: pointer;
}

.nav-item i {
    color: #fff;
    font-size: 20px;
    margin-bottom: 4px;
    transition: all 0.3s ease;
}

.nav-item span {
    font-size: 12px;
    transition: all 0.3s ease;
}

.nav-item.active {
    color: #fff;
}

.nav-item.active i {
    color: #fff;
    transform: translateY(-2px);
}

.nav-item:hover {
    color: #FFD700;
    transform: translateY(-2px);
}

/* Animations */
@keyframes pulse {
    0% { opacity: 1; }
    50% { opacity: 0.5; }
    100% { opacity: 1; }
}

@keyframes messageSlide {
    from {
        opacity: 0;
        transform: translateY(10px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

/* Responsive Styles */
@media (max-width: 768px) {
    .chatbot-container {
        height: calc(100vh - 60px);
    }

    .chat-messages {
        bottom: 70px;
    }

    .chat-input-container {
        bottom: 60px;
    }

    .connect-wallet {
        padding: 8px 16px;
        font-size: 0.9em;
    }
}

@media (max-width: 480px) {
    .header {
        padding: 8px 12px;
    }

    .logo {
        font-size: 1.5em;
    }

    .connect-wallet {
        padding: 8px 14px;
        font-size: 0.85em;
    }

    .chat-messages {
        padding: 15px;
    }

    .message {
        max-width: 90%;
    }

    .message-content {
        font-size: 0.9em;
    }

    .nav-item i {
        font-size: 18px;
    }

    .nav-item span {
        font-size: 11px;
    }
}

/* Dark mode optimization */
@media (prefers-color-scheme: dark) {
    .chatbot-container {
        background: rgba(26, 26, 31, 0.98);
    }
    
    .chat-input-container,
    .header,
    .bottom-nav {
        background: rgba(26, 26, 31, 0.98);
    }
}

/* Ensure proper spacing for messages near the bottom */
.chat-messages .message:last-child {
    margin-bottom: 16px;
}
    </style>
</head>
<body>
    <!-- Header -->
    <header class="header">
        <div class="header-content">
            <div class="logo">Deep</div>
            <button class="connect-wallet">
                <i class="fas fa-wallet"></i>
                Connect
            </button>
        </div>
    </header>

    <!-- Chatbot -->
    <div class="chatbot-container">
        <div class="chat-header">
            <div class="chat-status">
                <span class="status-dot"></span>
                Deep AI Assistant
            </div>
            <div class="chat-actions">
            </div>
        </div>
        <div class="chat-messages" id="chatMessages">
            <div class="message bot-message">
                <div class="message-avatar">
                    <i class="fas fa-robot"></i>
                </div>
                <div class="message-content">
                    <p>Hello! I'm your Web3 assistant. How can I help you explore the blockchain universe today?</p>
                </div>
            </div>
        </div>
        <div class="chat-input-container">
            <input type="text" id="chatInput" placeholder="Search Electrician, Plumber..." />
            <div class="input-actions">
                <button class="select-input">
                    <i class="fas fa-briefcase"></i>
                </button>
                <button class="send-message">
                    <i class="fas fa-paper-plane"></i>
                </button>
            </div>
        </div>
    </div>

<!-- Bottom Navigation -->
<nav class="bottom-nav">
    <div class="nav-container">
        <div class="nav-item active" data-page="home">
            <a href="https://nysaabhi.github.io/chat">
                <i class="fas fa-home"></i>
            </a>
            <span>Home</span>
        </div>
        <div class="nav-item" data-page="tournament">
            <a href="https://nysaabhi.github.io/mymom">
                <i class="fas fa-trophy"></i>
            </a>
            <span>Tournament</span>
        </div>
        <div class="nav-item" data-page="gallery">
            <a href="gallery.html">
                <i class="fas fa-vr-cardboard"></i>
            </a>
            <span>Gallery</span>
        </div>
        <div class="nav-item" data-page="location">
            <a href="location.html">
                <i class="fas fa-map"></i>
            </a>
            <span>Location</span>
        </div>
        <div class="nav-item" data-page="listings">
            <a href="listings.html">
                <i class="fas fa-list"></i>
            </a>
            <span>Listings</span>
        </div>
    </div>
</nav>

    <script>

</script>
</body>
