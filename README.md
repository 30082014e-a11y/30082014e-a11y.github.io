<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>Ambient | Атмосферное сообщество</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,300;14..32,400;14..32,500;14..32,600&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: linear-gradient(145deg, #0a0c12 0%, #10141f 100%);
            font-family: 'Inter', system-ui, -apple-system, 'Segoe UI', sans-serif;
            color: #eef2ff;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: flex-start;
            padding: 2rem 1.5rem 4rem;
            position: relative;
        }

        body::before {
            content: "";
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle at 20% 30%, rgba(80, 70, 140, 0.08) 0%, rgba(10, 12, 20, 0) 70%);
            pointer-events: none;
            z-index: 0;
        }

        .container {
            max-width: 780px;
            width: 100%;
            position: relative;
            z-index: 2;
            animation: fadeInUp 0.7s ease-out;
        }

        .ambient-title {
            text-align: center;
            margin-top: 0;
            margin-bottom: 2rem;
        }

        .ambient-title h1 {
            font-size: clamp(3.2rem, 12vw, 5.5rem);
            font-weight: 500;
            letter-spacing: 0.12em;
            background: linear-gradient(135deg, #FFFFFF 0%, #b7c9ff 80%);
            background-clip: text;
            -webkit-background-clip: text;
            color: transparent;
            text-shadow: 0 2px 5px rgba(0,0,0,0.2);
        }

        .description-card {
            background: rgba(18, 22, 35, 0.65);
            backdrop-filter: blur(12px);
            border-radius: 2rem;
            padding: 2rem 2rem;
            margin-bottom: 2.5rem;
            border: 1px solid rgba(110, 130, 200, 0.25);
            box-shadow: 0 20px 35px -12px rgba(0,0,0,0.4);
            transition: transform 0.2s ease, border-color 0.2s;
        }

        .description-card:hover {
            border-color: rgba(140, 170, 255, 0.5);
        }

        .ambient-text {
            font-size: 1.2rem;
            line-height: 1.65;
            font-weight: 400;
            color: #e9edff;
            text-align: center;
        }

        .ambient-text .fancy {
            font-size: 1.5rem;
            font-weight: 500;
            display: inline-block;
            background: linear-gradient(120deg, #f0e6ff, #c0d0ff);
            background-clip: text;
            -webkit-background-clip: text;
            color: transparent;
            letter-spacing: 0.01em;
        }

        .ambient-text p {
            margin-bottom: 1rem;
        }

        .ambient-text p:last-child {
            margin-bottom: 0;
        }

        .discord-widget {
            background: rgba(10, 12, 20, 0.7);
            backdrop-filter: blur(16px);
            border-radius: 1.8rem;
            border: 1px solid rgba(88, 101, 242, 0.5);
            overflow: hidden;
            transition: all 0.25s;
            margin-top: 1rem;
        }

        .widget-header {
            display: flex;
            align-items: center;
            gap: 1rem;
            padding: 1.2rem 1.8rem;
            background: rgba(32, 36, 50, 0.7);
            border-bottom: 1px solid rgba(114, 137, 218, 0.4);
        }

        .guild-icon {
            width: 56px;
            height: 56px;
            border-radius: 50%;
            background: #2c2f3f;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2rem;
            overflow: hidden;
            box-shadow: 0 4px 12px rgba(0,0,0,0.3);
        }

        .guild-icon img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .guild-info {
            flex: 1;
        }

        .guild-name {
            font-size: 1.55rem;
            font-weight: 600;
            letter-spacing: -0.3px;
            background: linear-gradient(125deg, #ffffff, #b9cbff);
            background-clip: text;
            -webkit-background-clip: text;
            color: transparent;
        }

        .guild-stats {
            display: flex;
            gap: 1rem;
            margin-top: 6px;
            font-size: 0.85rem;
            color: #adb7e0;
        }

        .stat {
            display: flex;
            align-items: center;
            gap: 0.3rem;
        }

        .widget-content {
            padding: 1.6rem 1.8rem;
            text-align: center;
        }

        .invite-button {
            display: inline-flex;
            align-items: center;
            gap: 0.6rem;
            background: #5865F2;
            padding: 0.85rem 2rem;
            border-radius: 3rem;
            font-weight: 600;
            font-size: 1rem;
            color: white;
            text-decoration: none;
            transition: all 0.2s ease;
            box-shadow: 0 6px 14px rgba(88, 101, 242, 0.3);
            border: none;
            cursor: pointer;
        }

        .invite-button:hover {
            background: #4752c4;
            transform: scale(1.02);
            box-shadow: 0 8px 20px rgba(88, 101, 242, 0.5);
        }

        .permanent-link {
            margin-top: 1rem;
            font-size: 0.9rem;
            display: flex;
            justify-content: center;
            gap: 0.5rem;
            align-items: center;
            flex-wrap: wrap;
            border-top: 1px dashed rgba(114, 137, 218, 0.3);
            padding-top: 1rem;
        }

        .permanent-link a {
            color: #b7c9ff;
            text-decoration: none;
            font-weight: 500;
            border-bottom: 1px dotted #6f8eff;
        }

        .permanent-link a:hover {
            color: white;
            border-bottom-color: white;
        }

        .loading-state, .error-state {
            padding: 2rem;
            text-align: center;
            color: #b9c8ff;
        }

        .error-state {
            color: #ffb4a2;
        }

        .spinner {
            display: inline-block;
            width: 28px;
            height: 28px;
            border: 3px solid rgba(88, 101, 242, 0.3);
            border-radius: 50%;
            border-top-color: #5865F2;
            animation: spin 0.8s linear infinite;
            margin-bottom: 1rem;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @media (max-width: 600px) {
            body {
                padding: 1.5rem 1rem 2rem;
            }
            .description-card {
                padding: 1.5rem;
            }
            .ambient-text {
                font-size: 1rem;
            }
            .widget-header {
                flex-direction: column;
                text-align: center;
                padding: 1.2rem;
            }
            .guild-stats {
                justify-content: center;
            }
            .widget-content {
                padding: 1.2rem;
            }
            .invite-button {
                padding: 0.7rem 1.5rem;
                font-size: 0.9rem;
            }
        }

        footer {
            text-align: center;
            margin-top: 3rem;
            font-size: 0.75rem;
            opacity: 0.5;
            color: #8d9ad0;
        }
    </style>
</head>
<body>
<div class="container">
    <div class="ambient-title">
        <h1>Ambient</h1>
    </div>

    <div class="description-card">
        <div class="ambient-text">
            <p><span class="fancy">𝒜𝓂𝒷𝒾𝑒𝓃𝒯</span> — здесь играет фоновая музыка и звучат совместные партии.<br>
            Мы объединяем игроков, которые ценят атмосферу в играх: от релакс-симуляторов до глубоких RPG. Вместе исследуем миры, делимся саундтреками и создаём уют.<br>
            Если для тебя игра — это больше, чем просто механики, тебе к нам!</p>
        </div>
    </div>

    <div class="discord-widget" id="discordWidget">
        <div class="loading-state" id="widgetLoading">
            <div class="spinner"></div>
            <div>Загружаем атмосферу сообщества...</div>
        </div>
        <div id="widgetContent" style="display: none;"></div>
    </div>
    <footer>♫ ambient community — уютные партии & звуковые пейзажи</footer>
</div>

<script>
    // Постоянная ссылка на сервер (по заданию)
    const PERMANENT_INVITE_URL = "https://discord.gg/YDEETdXBtd";
    const WIDGET_JSON_URL = "https://discord.com/api/guilds/1486642688034996318/widget.json";

    async function loadDiscordWidget() {
        const loadingDiv = document.getElementById('widgetLoading');
        const contentDiv = document.getElementById('widgetContent');

        try {
            const response = await fetch(WIDGET_JSON_URL, {
                method: 'GET',
                headers: { 'Accept': 'application/json' }
            });

            if (!response.ok) {
                throw new Error(`Ошибка HTTP ${response.status}: не удалось загрузить виджет. Возможно, виджет сервера отключён.`);
            }

            const data = await response.json();
            if (!data || !data.id) {
                throw new Error('Невалидные данные от Discord API');
            }

            const guildName = data.name || 'Ambient Server';
            const memberCount = data.members ? data.members.length : (data.presence_count || '—');
            const onlineCount = data.presence_count !== undefined ? data.presence_count : (data.members ? data.members.filter(m => m.status === 'online' || m.status === 'idle' || m.status === 'dnd').length : '—');
            const iconHash = data.icon ? data.icon : null;
            let iconUrl = null;
            if (iconHash) {
                iconUrl = `https://cdn.discordapp.com/icons/${data.id}/${iconHash}.png?size=128`;
            }

            renderWidget(guildName, memberCount, onlineCount, iconUrl);
            loadingDiv.style.display = 'none';
            contentDiv.style.display = 'block';

        } catch (error) {
            console.error('Ошибка загрузки виджета Discord:', error);
            loadingDiv.innerHTML = `
                <div class="error-state">
                    <div style="font-size: 2rem; margin-bottom: 0.5rem;">✨</div>
                    <div>Не удалось подключиться к виджету сервера.</div>
                    <div style="font-size: 0.85rem; margin-top: 0.8rem;">${error.message}</div>
                    <div style="margin-top: 1rem; font-size: 0.8rem;">Но ты всегда можешь найти нас через Discord!</div>
                    <div class="permanent-link" style="border-top: none; margin-top: 1rem;">
                        🔗 <a href="${PERMANENT_INVITE_URL}" target="_blank" rel="noopener noreferrer">Присоединиться к Ambient по постоянной ссылке</a>
                    </div>
                </div>
            `;
        }
    }

    function renderWidget(guildName, memberCount, onlineCount, iconUrl) {
        const widgetContainer = document.getElementById('widgetContent');
        if (!widgetContainer) return;

        const formatCount = (count) => {
            if (typeof count === 'number') return count;
            if (count === '—') return '—';
            return count;
        };

        const membersDisplay = typeof memberCount === 'number' ? memberCount : memberCount;
        const onlineDisplay = typeof onlineCount === 'number' ? onlineCount : onlineCount;

        widgetContainer.innerHTML = `
            <div class="widget-header">
                <div class="guild-icon">
                    ${iconUrl ? `<img src="${iconUrl}" alt="иконка сервера" loading="lazy">` : '🎧'}
                </div>
                <div class="guild-info">
                    <div class="guild-name">${escapeHtml(guildName)}</div>
                    <div class="guild-stats">
                        <div class="stat">👥 Участников: ${formatCount(membersDisplay)}</div>
                        <div class="stat">🟢 В сети: ${formatCount(onlineDisplay)}</div>
                    </div>
                </div>
            </div>
            <div class="widget-content">
                <!-- Основная кнопка с ПОСТОЯННОЙ ссылкой (добавлено по заданию) -->
                <a href="${PERMANENT_INVITE_URL}" target="_blank" rel="noopener noreferrer" class="invite-button">
                    ✦ Присоединиться к Ambient ✦
                </a>
                <div class="permanent-link">
                    <span>🎵 постоянное приглашение в уютное сообщество</span>
                </div>
                <p style="font-size: 0.7rem; margin-top: 1rem; opacity: 0.6;">музыка, релакс, совместные партии и глубокие RPG</p>
            </div>
        `;
    }

    function escapeHtml(str) {
        if (!str) return '';
        return str.replace(/[&<>]/g, function(m) {
            if (m === '&') return '&amp;';
            if (m === '<') return '&lt;';
            if (m === '>') return '&gt;';
            return m;
        }).replace(/[\uD800-\uDBFF][\uDC00-\uDFFF]/g, function(c) {
            return c;
        });
    }

    window.addEventListener('DOMContentLoaded', () => {
        loadDiscordWidget();
    });
</script>
</body>
</html>
