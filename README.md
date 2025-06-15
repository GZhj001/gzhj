<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes">
    <title>中三班美食播报 - 郭昊鑫</title>
    <link href="https://fonts.googleapis.com/css2?family=Ma+Shan+Zheng&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #ff9800;
            --primary-dark: #ff5722;
            --accent: #ffb300;
            --accent-light: #fff9c4;
            --text-dark: #5d4037;
            --text-light: #8d6e63;
            --success: #4caf50;
            --success-light: #8bc34a;
            --white: #ffffff;
            --light-bg: #fff8e1;
            --shadow: 0 10px 30px rgba(255, 152, 0, 0.15);
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        html, body {
            height: 100%;
            overflow-x: hidden;
        }
        
        body {
            background: linear-gradient(135deg, #fff9c4 0%, #ffecb3 100%);
            padding: 15px;
            display: flex;
            justify-content: center;
            align-items: flex-start;
            font-family: 'Comic Sans MS', 'Ma Shan Zheng', '微软雅黑', sans-serif;
            color: var(--text-dark);
            line-height: 1.6;
            min-height: 100%;
            position: relative;
        }
        
        .container {
            max-width: 900px;
            width: 100%;
            background: var(--white);
            border-radius: 20px;
            box-shadow: 0 12px 30px rgba(255, 152, 0, 0.2);
            overflow: visible;
            position: relative;
            margin: 0 auto;
        }
        
        /* 顶部横幅 - 移动端优化 */
        .header {
            background: linear-gradient(90deg, var(--primary) 0%, var(--primary-dark) 100%);
            padding: 20px 15px 35px;
            text-align: center;
            position: relative;
            overflow: visible;
            z-index: 5;
        }
        
        .header::before {
            content: "";
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255,255,255,0.1) 0%, rgba(255,255,255,0) 70%);
            transform: rotate(30deg);
        }
        
        .header h1 {
            color: var(--white);
            font-size: clamp(1.5rem, 6vw, 2.2rem);
            text-shadow: 0 2px 4px rgba(0,0,0,0.2);
            letter-spacing: 1px;
            position: relative;
            z-index: 2;
            margin-bottom: 10px;
            line-height: 1.3;
            padding: 0 10px;
        }
        
        .header .subtitle {
            color: #fffde7;
            font-size: clamp(1rem, 4vw, 1.4rem);
            position: relative;
            z-index: 2;
            display: block;
            padding: 0 10px;
            line-height: 1.6;
            margin-top: 5px;
        }
        
        /* 播报员卡片 - 移动端优化 */
        .reporter-card {
            background: var(--white);
            width: 92%;
            max-width: 600px;
            margin: -25px auto 20px;
            padding: 18px;
            border-radius: 18px;
            box-shadow: var(--shadow);
            text-align: center;
            position: relative;
            z-index: 10;
        }
        
        .avatar {
            width: 85px;
            height: 85px;
            border-radius: 50%;
            background: #ffecb3;
            margin: 0 auto 12px;
            display: flex;
            justify-content: center;
            align-items: center;
            border: 4px solid var(--primary);
            position: relative;
            overflow: hidden;
        }
        
        .avatar::before {
            content: "🍳";
            font-size: 2.6rem;
            animation: bounce 2s ease-in-out infinite;
        }
        
        .reporter-card h2 {
            color: var(--primary-dark);
            font-size: clamp(1.6rem, 5vw, 2rem);
            margin-bottom: 6px;
        }
        
        .reporter-card p {
            color: var(--text-dark);
            font-size: clamp(0.9rem, 3vw, 1.1rem);
            line-height: 1.5;
        }
        
        /* 美食时间线 - 移动端优化 */
        .timeline {
            padding: 0 15px 20px;
            overflow: visible;
        }
        
        .meal-card {
            background: var(--light-bg);
            border-left: 5px solid var(--accent);
            border-radius: 0 15px 15px 0;
            padding: 16px;
            margin-bottom: 20px;
            position: relative;
            transition: all 0.3s ease;
        }
        
        .meal-card:hover {
            transform: translateY(-5px);
            background: #fff3cc;
            box-shadow: 0 10px 20px rgba(255, 152, 0, 0.12);
        }
        
        .time-tag {
            position: absolute;
            top: 12px;
            right: 12px;
            background: var(--accent);
            color: var(--white);
            padding: 4px 10px;
            border-radius: 18px;
            font-weight: bold;
            font-size: 0.75rem;
        }
        
        .meal-card h3 {
            color: var(--primary-dark);
            font-size: clamp(1.3rem, 4vw, 1.6rem);
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 8px;
            padding-right: 80px;
        }
        
        .meal-card h3::before {
            content: "";
            display: inline-block;
            width: 24px;
            height: 24px;
            background-repeat: no-repeat;
            background-size: contain;
        }
        
        .breakfast h3::before { 
            background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path fill="%23ff6d00" d="M18 7c0-2.8-2.2-5-5-5S8 4.2 8 7c0 .7.2 1.4.5 2H6c-2.2 0-4 1.8-4 4v1h2v7c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2v-7h2v-1c0-2.2-1.8-4-4-4h-2.5c.3-.6.5-1.3.5-2zm-6-3c1.7 0 3 1.3 3 3s-1.3 3-3 3-3-1.3-3-3 1.3-3 3-3zM4 14h16v3c0 .6-.4 1-1 1H5c-.6 0-1-.4-1-1v-3z"/></svg>'); 
        }
        
        .snack h3::before { 
            background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path fill="%23ff6d00" d="M17.2 13c-.6-1.4-1.6-2.5-3-3.1-.5-1.4-1.2-2.7-2.2-3.7-.9-.9-2-1.6-3.2-2-1.3 1.3-2 3-2 4.8 0 1.8.7 3.5 2 4.8l-1.4 1.4c-1.5-1.5-2.6-3.6-2.6-6.2 0-2.6 1.1-4.7 2.6-6.2L7.7 3c1.8 1.8 3 4.3 3 7 0 2.7-1.2 5.2-3 7l-1.4-1.4c1.5-1.5 2.4-3.6 2.4-5.6 0-2-.9-4.1-2.4-5.6-.7 2-1 4.1-1 6.2 0 2.1.3 4.2 1 6.2l1.4-1.4c-.6-1.6-.9-3.3-.9-4.8 0-1.5.3-3.2.9-4.8 1.1.4 2 .9 2.8 1.7.7.7 1.3 1.6 1.7 2.6l6 6c.4.4.4 1 0 1.4s-1 .4-1.4 0l-5.3-5.3-1.4 1.4 5.3 5.3c.4.4 1 .4 1.4 0s.4-1 0-1.4l-5.3-5.3c.4-.4.8-.7 1.2-1.1 1.1-.8 2-1.9 2.7-3.1z"/></svg>'); 
        }
        
        .lunch h3::before { 
            background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path fill="%23ff6d00" d="M12 3c-4.4 0-8 3.6-8 8 0 2.3 1.1 4.4 3 5.7V21h10v-4.3c1.9-1.3 3-3.4 3-5.7 0-4.4-3.6-8-8-8zm3 11.3c-.6.4-1.3.7-2 .7s-1.4-.3-2-.7V20H9v-3.8c-1.2-1.1-2-2.7-2-4.2 0-3.3 2.7-6 6-6s6 2.7 6 6c0 1.5-.7 3.1-2 4.2V20h-2v-5.7z"/></svg>'); 
        }
        
        .afternoon h3::before { 
            background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path fill="%23ff6d00" d="M16 13c-1.7 0-3 1.3-3 3s1.3 3 3 3 3-1.3 3-3-1.3-3-3-3zm0 4c-.6 0-1-.4-1-1s.4-1 1-1 1 .4 1 1-.4 1-1 1zm-8-4c-1.7 0-3 1.3-3 3s1.3 3 3 3 3-1.3 3-3-1.3-3-3-3zm0 4c-.6 0-1-.4-1-1s.4-1 1-1 1 .4 1 1-.4 1-1 1zM16 4c-.3 0-.5 0-.8.1l-2.2-2.2c-.4-.4-1-.4-1.4 0s-.4 1 0 1.4l.9.9C10.2 4.5 9.1 5 8 5c-2.8 0-5 2.2-5 5s2.2 5 5 5c1.1 0 2.2-.5 3-1.3.6.5 1.3.9 2.1 1.1.5-1.7 2-3 3.9-3 2.2 0 4 1.8 4 4s-1.8 4-4 4c-.3 0-.6 0-.9-.1l-2.2 2.2c-.4.4-.4 1 0 1.4.2.2.5.3.7.3s.5-.1.7-.3l.9-.9c.8.7 1.9 1.2 3 1.2 2.8 0 5-2.2 5-5s-2.2-5-5-5z"/></svg>'); 
        }
        
        .food-list {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
            gap: 10px;
            margin-top: 10px;
        }
        
        .food-item {
            background: var(--white);
            border-radius: 10px;
            padding: 10px;
            text-align: center;
            box-shadow: 0 3px 8px rgba(255, 152, 0, 0.1);
            transition: all 0.3s ease;
        }
        
        .food-item:hover {
            box-shadow: 0 5px 12px rgba(255, 152, 0, 0.2);
            transform: translateY(-3px);
        }
        
        .food-icon {
            font-size: 2rem;
            margin-bottom: 6px;
            display: inline-block;
        }
        
        .food-name {
            color: var(--text-dark);
            font-weight: bold;
            margin-bottom: 4px;
            font-size: 0.95rem;
        }
        
        .food-desc {
            color: var(--text-light);
            font-size: 0.8rem;
        }
        
        /* 光盘行动 - 移动端优化 */
        .cd-action {
            background: linear-gradient(90deg, var(--success) 0%, var(--success-light) 100%);
            padding: 18px 20px;
            margin: 15px;
            border-radius: 15px;
            color: var(--white);
            text-align: center;
            position: relative;
            overflow: hidden;
        }
        
        .cd-action::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="60" height="60" opacity="0.1"><path fill="%23ffffff" d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-2 15l-5-5 1.41-1.41L10 14.17l7.59-7.59L19 8l-9 9z"/></svg>');
        }
        
        .cd-action h3 {
            font-size: clamp(1.4rem, 4vw, 1.8rem);
            margin-bottom: 12px;
            display: flex;
            justify-content: center;
            align-items: center;
            position: relative;
        }
        
        .cd-action h3::after {
            content: "🌟";
            margin-left: 8px;
        }
        
        .cd-action p {
            font-size: clamp(0.95rem, 3vw, 1.1rem);
            line-height: 1.6;
            margin-bottom: 10px;
            position: relative;
        }
        
        .cd-badge {
            display: inline-block;
            background: #ffeb3b;
            color: var(--success);
            padding: 7px 18px;
            border-radius: 25px;
            font-weight: bold;
            font-size: clamp(1rem, 3vw, 1.2rem);
            margin-top: 6px;
            position: relative;
            box-shadow: 0 3px 6px rgba(0,0,0,0.1);
        }
        
        /* 古诗区域 - 移动端优化（重点优化） */
        .poem-section {
            background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="100" height="100" viewBox="0 0 100 100"><path fill="%23f5f5f5" d="M50,0C22.4,0,0,22.4,0,50s22.4,50,50,50s50-22.4,50-50S77.6,0,50,0z M50,92C27.9,92,10,74.1,10,52S27.9,12,50,12 s40,17.9,40,40S72.1,92,50,92z"/></svg>');
            background-size: 40px;
            padding: 25px 15px;
            text-align: center;
            border-top: 3px dashed #ffccbc;
        }
        
        .poem-title {
            color: var(--text-dark);
            font-size: clamp(1.6rem, 5vw, 2.2rem);
            margin-bottom: 12px;
            position: relative;
            display: inline-block;
            font-family: 'Ma Shan Zheng', cursive;
        }
        
        .poem-title::after {
            content: "";
            position: absolute;
            bottom: -6px;
            left: 50%;
            transform: translateX(-50%);
            width: 50px;
            height: 3px;
            background: var(--primary);
        }
        
        .poem-author {
            color: var(--text-light);
            font-size: clamp(0.95rem, 3vw, 1.2rem);
            margin-bottom: 15px;
        }
        
        .poem-content {
            max-width: 600px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.92);
            padding: 20px;
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.05);
            position: relative;
            backdrop-filter: blur(2px);
        }
        
        .poem-content::before {
            content: """" "";
            position: absolute;
            top: -12px;
            left: 50%;
            transform: translateX(-50%);
            width: 45px;
            height: 45px;
            background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path fill="%23ff9800" d="M18.8 11.5c-1.2-1.9-3.3-3.2-5.6-3.5.4-1.2.7-2.5.7-3.8 0-1.2-.2-2.4-.7-3.5-.5.8-.7 1.7-.7 2.6 0 1.2.3 2.4.8 3.5-1.1.3-2 .9-2.7 1.7-1.7-1.9-4.4-2.8-7.1-2.3-1.4.3-2.7 1-3.6 2.1-.9 1.1-1.4 2.4-1.4 3.8 0 3.3 2.7 6 6 6h12c1.1 0 2.2-.4 3-1.2.8-.8 1.2-1.9 1.2-3 0-1.5-.7-2.8-1.9-3.6zM6 12c-2.2 0-4-1.8-4-4s1.8-4 4-4 4 1.8 4 4-1.8 4-4 4zm16 4H10c-1.1 0-2 .9-2 2v4c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2v-4c0-1.1-.9-2-2-2zm-2 6h-8v-2h8v2z"/></svg>') center/contain no-repeat;
        }
        
        .poem-text {
            font-family: 'Ma Shan Zheng', '楷体', 'STKaiti', serif;
            color: var(--text-dark);
            margin-bottom: 15px;
            letter-spacing: 1px;
        }
        
        .poem-line {
            display: block;
            font-size: clamp(1.2rem, 4.5vw, 1.6rem);
            line-height: 1.8;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
            text-align: center;
            margin: 8px 0;
        }
        
        .poem-meaning {
            font-size: clamp(0.9rem, 3vw, 1rem);
            color: var(--text-light);
            line-height: 1.5;
            font-style: italic;
            border-top: 1px dashed #bcaaa4;
            padding-top: 12px;
        }
        
        /* 页脚 - 移动端优化 */
        .footer {
            background: var(--text-dark);
            color: #ffccbc;
            text-align: center;
            padding: 20px 15px;
            font-size: clamp(0.9rem, 3vw, 1rem);
        }
        
        .closing {
            font-size: clamp(1.3rem, 4vw, 1.5rem);
            margin-bottom: 10px;
            color: var(--white);
            font-weight: bold;
        }
        
        /* 动画优化 */
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
        
        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-8px); }
        }
        
        @keyframes float {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-6px); }
        }
        
        .food-icon {
            animation: float 3s ease-in-out infinite;
        }
        
        .delay-1 { animation-delay: 0.2s; }
        .delay-2 { animation-delay: 0.4s; }
        .delay-3 { animation-delay: 0.6s; }
        .delay-4 { animation-delay: 0.8s; }
        
        .cd-badge {
            animation: pulse 2s ease-in-out infinite;
        }
        
        /* 响应式设计 - 重点优化移动端 */
        @media (max-width: 768px) {
            .reporter-card { 
                margin-top: -25px; 
                padding: 15px;
            }
            
            .avatar {
                width: 80px;
                height: 80px;
            }
            
            .timeline {
                padding: 0 12px 15px;
            }
            
            .meal-card {
                padding: 14px;
                margin-bottom: 18px;
            }
            
            .cd-action {
                margin: 12px;
                padding: 16px;
            }
            
            .food-list {
                grid-template-columns: repeat(auto-fit, minmax(130px, 1fr));
                gap: 8px;
            }
        }
        
        @media (max-width: 480px) {
            body {
                padding: 10px;
                align-items: flex-start;
            }
            
            .container {
                border-radius: 18px;
            }
            
            .header {
                padding: 18px 12px 30px;
            }
            
            .header h1 {
                font-size: 1.6rem;
                line-height: 1.4;
            }
            
            .header .subtitle {
                font-size: 1.1rem;
                line-height: 1.6;
            }
            
            .reporter-card {
                margin-top: -20px;
                width: 94%;
            }
            
            .food-list {
                grid-template-columns: 1fr 1fr;
            }
            
            .food-item {
                padding: 8px;
            }
            
            .food-icon {
                font-size: 1.8rem;
            }
            
            .food-name {
                font-size: 0.9rem;
            }
            
            .food-desc {
                font-size: 0.75rem;
            }
            
            .poem-section {
                padding: 20px 10px;
            }
            
            .poem-content {
                padding: 18px 12px;
            }
            
            .poem-line {
                font-size: 1.3rem;
                line-height: 1.6;
            }
            
            .footer {
                padding: 18px 12px;
            }
        }
        
        @media (max-width: 360px) {
            .header h1 {
                font-size: 1.5rem;
            }
            
            .header .subtitle {
                font-size: 1rem;
            }
            
            .reporter-card h2 {
                font-size: 1.4rem;
            }
            
            .food-list {
                grid-template-columns: 1fr;
            }
            
            .meal-card h3 {
                padding-right: 70px;
            }
            
            .time-tag {
                font-size: 0.7rem;
                padding: 3px 8px;
            }
            
            .poem-line {
                font-size: 1.2rem;
                white-space: normal;
                overflow: visible;
                text-overflow: clip;
            }
        }
        
        /* 滚动条美化 */
        ::-webkit-scrollbar {
            width: 8px;
        }
        
        ::-webkit-scrollbar-track {
            background: #ffecb3;
            border-radius: 4px;
        }
        
        ::-webkit-scrollbar-thumb {
            background: #ffb300;
            border-radius: 4px;
        }
        
        ::-webkit-scrollbar-thumb:hover {
            background: #ff9800;
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- 顶部横幅 - 移动端优化 -->
        <div class="header">
            <h1>🍽️ 双柏县西城幼儿园美食播报</h1>
            <div class="subtitle">营养均衡 · 健康成长 · 光盘行动</div>
        </div>
        
        <!-- 小播报员卡片 - 移动端优化 -->
        <div class="reporter-card">
            <div class="avatar"></div>
            <h2>郭昊鑫</h2>
            <p>中三班小小美食播报员 · 2025年6月18日</p>
        </div>
        
        <!-- 美食时间线 - 移动端优化 -->
        <div class="timeline">
            <!-- 早餐 -->
            <div class="meal-card breakfast">
                <div class="time-tag">7:50-8:20 AM</div>
                <h3>美味早餐</h3>
                <div class="food-list">
                    <div class="food-item">
                        <div class="food-icon">🦋</div>
                        <div class="food-name">蝴蝶面</div>
                        <div class="food-desc">像小蝴蝶一样可爱</div>
                    </div>
                    <div class="food-item">
                        <div class="food-icon">🥚</div>
                        <div class="food-name">营养鸡蛋</div>
                        <div class="food-desc">圆滚滚的能量来源</div>
                    </div>
                </div>
            </div>
            
            <!-- 课间点 -->
            <div class="meal-card snack">
                <div class="time-tag">10:00 AM</div>
                <h3>课间加餐</h3>
                <div class="food-list">
                    <div class="food-item">
                        <div class="food-icon">🌰</div>
                        <div class="food-name">混合坚果</div>
                        <div class="food-desc">香香脆脆 活力满满</div>
                    </div>
                </div>
            </div>
            
            <!-- 午餐 -->
            <div class="meal-card lunch">
                <div class="time-tag">11:30 -12:30AM</div>
                <h3>营养午餐</h3>
                <div class="food-list">
                    <div class="food-item">
                        <div class="food-icon">🍗</div>
                        <div class="food-name">黄焖鸡</div>
                        <div class="food-desc">鸡肉软软的很好吃</div>
                    </div>
                    <div class="food-item">
                        <div class="food-icon">🍅</div>
                        <div class="food-name">西红柿炒鸡蛋</div>
                        <div class="food-desc">红彤彤的 酸酸甜甜</div>
                    </div>
                    <div class="food-item">
                        <div class="food-icon">🍈</div>
                        <div class="food-name">蒸香瓜</div>
                        <div class="food-desc">软软甜甜好味道</div>
                    </div>
                    <div class="food-item">
                        <div class="food-icon">🍜</div>
                        <div class="food-name">白菜粉丝汤</div>
                        <div class="food-desc">暖暖的 很贴心</div>
                    </div>
                    <div class="food-item">
                        <div class="food-icon">🍚</div>
                        <div class="food-name">白米饭</div>
                        <div class="food-desc">香喷喷的能量主食</div>
                    </div>
                </div>
            </div>
            
            <!-- 午点 -->
            <div class="meal-card afternoon">
                <div class="time-tag">3:00 PM</div>
                <h3>午后点心</h3>
                <div class="food-list">
                    <div class="food-item">
                        <div class="food-icon">🥛</div>
                        <div class="food-name">甜牛奶</div>
                        <div class="food-desc">香甜补钙 帮助长高</div>
                    </div>
                    <div class="food-item">
                        <div class="food-icon">🍪</div>
                        <div class="food-name">小饼干</div>
                        <div class="food-desc">酥脆可口 能量补充</div>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- 光盘行动 - 移动端优化 -->
        <div class="cd-action">
            <h3>老师的话要牢记</h3>
            <p>吃饭要乖乖坐好，细嚼慢咽不挑食</p>
            <p>这样才能长得高高壮壮，变成健康小超人！</p>
            <div class="cd-badge">争当"光盘小明星"</div>
        </div>
        
        <!-- 古诗区域 - 移动端优化（重点优化） -->
        <div class="poem-section">
            <h2 class="poem-title">悯农</h2>
            <div class="poem-author">作者 · 李绅</div>
            
            <div class="poem-content">
                <div class="poem-text">
                    <span class="poem-line">锄禾日当午，汗滴禾下土。</span>
                    <span class="poem-line">谁知盘中餐，粒粒皆辛苦。</span>
                </div>
                <div class="poem-meaning">
                    古诗通过描绘农民烈日下劳作的艰辛，呼吁珍惜粮食、尊重劳动，每一粒粮食都来之不易，我们一定不能浪费粮食。
                </div>
            </div>
        </div>
        
        <!-- 页脚 - 移动端优化 -->
        <div class="footer">
            <div class="closing">谢谢大家！我的美食播报结束</div>
            <p>西城幼儿园中三班 · 让美食伴随健康成长</p>
            <p>珍惜粮食 尊重劳动 从我做起</p>
        </div>
    </div>

    <script>
        // 添加食物图标动画
        document.querySelectorAll('.food-icon').forEach((icon, index) => {
            icon.classList.add(`delay-${index % 4}`);
        });
        
        // 确保页面加载后滚动到顶部
        window.addEventListener('load', function() {
            window.scrollTo(0, 0);
        });
    </script>
</body>
</html>
